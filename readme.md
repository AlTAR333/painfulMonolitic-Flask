## TO DO LIST:

- 5 things to do here (should be painful and difficult to handle)

## The repo is a monolithic app:

- Flask + SQLite is the right call. Zero setup friction — students just pip install flask and run it. No Docker, no config.
- Pre-seeded data is essential. Students shouldn't have to populate it — they should immediately start hitting walls. Seed it with realistic interconnected data (users who have games, activities, notifications, friends).
- Keep it under 400 lines total. One app.py, one models.py or just raw SQL, one seed.py. The messiness should be architectural, not syntactic.
- The README is the exercise. A short list of tasks: "do these 5 things." No hints. Let them discover the pain themselves.

## Set up:

- pip install flask and run it
- pip install -r requirements.txt

## Proposed Structure

painfulMonolitic/
├── app.py # Everything in one file: routes, logic, DB queries
├── models.py # Raw SQLite schema — one big shared DB, FK constraints everywhere
├── seed.py # Pre-fills DB with realistic interconnected data
├── requirements.txt
├── README.md # THE EXERCISE — 5 tasks, no hints
└── .gitignore

---
