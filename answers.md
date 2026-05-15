**1. When a user logs a new activity, how many database tables are written to?**

Two databases are being written into : activities (the new activity row) and notifications (one row per friend of the acting user).


**2. You call DELETE FROM users WHERE id = 3 directly in SQLite. What happens, and why?**

Without PRAGMA foreign_keys = ON, the delete silently succeeds but it leaves some orphan rows in activities, notifications, friends, and user_games. With foreign keys on, it fails and sends a constraint error. Either way, you must first delete in order: notifications -> activities -> user_games -> friends -> user.


**3. User nova changes her username to nova_2. What do her friends see?**

They see the old name (nova). Notification messages are plain text made at creation time. Updating users.username does not rewrite them. Only the future notifications will show nova_2.


**4. Trace the full journey of a POST /activities request.**

1. Flask routes to create_activity()
2. JSON body is parsed for user_id, game_id, action
3. DB connection opened (PRAGMA foreign_keys = ON)
4. INSERT into activities, then commit()
5. New activity row re-fetched
6. Actor's username is fetched from users
7. Game title also fetched from games
8. Actor's friends fetched from friends
9. For each friend, we buid the notification message,  then INSERT into notifications
10. commit(), connection closed, activity returned as JSON 201


**5. pixel_queen opts out. Teammate adds opted_out column and checks it in POST /activities. Fully implemented?**

No. The activity + notification logic is duplicated in the two routes: POST /activities (the API) and POST /view/activities (the HTML form). If only one is patched, the other still logs the activities and sends notifications for opted-out users.


**6. How many rows are created when nova logs one activity?**

4 rows in total:
- 1 row in activities
- 3 rows in notifications because nova has 3 friends in the seed data: alex_g, maya_r, and pixel_queen


**7. In what order must you delete maya_r?**

1. DELETE FROM notifications WHERE user_id = <id> (she receives)
2. DELETE FROM notifications WHERE triggered_by = <id>
3. DELETE FROM activities WHERE user_id = <id>
4. DELETE FROM user_games WHERE user_id = <id>
5. DELETE FROM friends WHERE user_id = <id> OR friend_id = <id>
6. DELETE FROM users WHERE id = <id>

We need to do this order because of notifications.activity_id is a foreing key to activities, wich means notifications must be cleared before their parent activity can be deleted.


**8. What happens if you delete an activity that has notifications attached?**

2 things can happen
- With foreign keys on: the delete fails because of notifications. activity_id references activities(id). We must delete the notifications first.
- With foreign keys off: the delete succeeds but leaves notifications with an alone activity_id.


**9. You fix a game title and restart the app. What else went down?**

Everything. Users, auth, activity logging, notifications, and all API and HTML routes share the same process. A restart to ship a one-field fix causes a full outage for the entire duration of the restart, wich is very bad, and will be fixed hoppefuly next assignment.


**10. Does moving notification logic into its own function in app.py solve Task 4?**

No. It's just a cosmetic visual refactor. The notifications still run inside the activity handler, in the same process and DB transaction. The real problem is you can't disable, delay, or also independently deploy the notification system without touching the activity code. A good and proper fix would require "decoupling": a feature flag, an event queue, or a separate service.
