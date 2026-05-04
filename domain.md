# GameHub — Product Domain

## What is GameHub?

GameHub is a social platform for gamers. It lets players track what they are playing,
share their progress with friends, and discover what the community is into.
The idea is simple: gaming is more fun when it's social. You shouldn't need to text
your friends to find out what they've been playing — the platform should just show you.

Users build a personal game library, log activity as they play, and follow each other.
Every time someone starts or finishes a game, their friends hear about it automatically.

---

## The users

These are the five people who signed up when the platform launched.

**nova**
An explorer at heart. She jumps between genres constantly — one week it's a
metroidvania, the next it's a narrative adventure. She was the first user on the platform
and has the most varied game library.

**alex_g**
A speedrunner. He plays fewer games but goes deep — hundreds of hours in titles most
people complete in twenty. He's competitive, tracks everything, and always has an opinion
on whether a game is worth the time.

**maya_r**
An RPG lover obsessed with lore. She takes her time, reads every dialogue line, and
has completed Stardew Valley more times than she'll admit. She's the most active user
in terms of logged activities.

**thunderbyte**
Primarily an FPS player who occasionally wanders into cosy games and refuses to admit
he enjoys them. He's friends with alex_g and they compete over completion times.

**pixel_queen**
A completionist. If a game has achievements, she will get all of them. She has the
most hours logged on the platform and is quietly friends with everyone.

---

## What the platform does

- **Game library** — users add games to their personal library and track how many hours they've played
- **Activity feed** — users log what they're doing: started a game, completed it, replaying it, dropped it
- **Friends** — users follow each other and see a feed of their friends' activity
- **Notifications** — when a friend logs an activity, you get a notification automatically
- **Game catalog** — a shared list of all games on the platform that any user can browse

---

## How the data connects

Everything on GameHub is connected.

When **nova** logs that she started *Outer Wilds*, two things happen: her activity is
recorded, and all of her friends receive a notification about it. Those notifications
reference nova's account and the specific activity that triggered them.

When **alex_g** builds a library of games, each entry ties his account to a game in
the catalog. If that game is ever removed, his library entry goes with it. If his
account is removed, his library, his activities, and every notification he ever
triggered for his friends all need to go with it too.

Friends are mutual. If nova follows pixel_queen, pixel_queen also follows nova.
A friendship is a connection between two accounts — remove either account and
the connection breaks.

This web of relationships means that no piece of data exists in isolation.
A user is not just a name and an email. A user is a node in a network of
games, activities, friendships, and notifications — all of which depend on each other.

---

## The handover

GameHub was built quickly by a small team who needed to ship fast.
It works. Users are active. The data is real.

You've just joined the team. The original developers have moved on.
There is no documentation beyond what you're reading now, and a few tasks
have been sitting in the backlog waiting for someone to pick them up.

That someone is you.

Read the `readme.md` to get started.
