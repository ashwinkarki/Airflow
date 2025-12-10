# Airflow

Airflow Project README

This repository is currently an empty Airflow project scaffold. These notes will help you set up, organize, and run your Airflow environment.

📌 Project Overview

This repository will be used to build an Apache Airflow pipeline setup for scheduling, orchestrating, and monitoring

workflows.Repository Structure (Planned)

├── dags/ # DAG files will go here
├── plugins/ # Custom plugins (hooks, operators)
├── docker-compose.yml # If using Docker setup
├── requirements.txt # Python dependencies
└── README.md # Documentation (this file)

with DAG(
    dag_id="sample_dag",
    start_date=datetime(2025, 1, 1),
    schedule_interval="@daily",
    catchup=False,
) as dag:

✅ 1. dag_id

What it is:
A unique identifier for the DAG.

Why it matters:

Airflow uses this name to track runs, logs, scheduler, and UI display.

Must be unique within your Airflow environment.

Example:
"sample_dag" → This DAG will appear in the UI as sample_dag.

✅ 2. start_date

What it is:
The date & time when the DAG should start scheduling.

Important notes:

Airflow will not schedule any runs before this date.

It is not "when the DAG starts running right now", but the calendar start.

Example:
datetime(2025, 1, 1) → The DAG will consider runs starting from Jan 1, 2025.

✅ 3. schedule_interval

What it is:
Defines how often the DAG will run.

Common values:

"@daily" → every day at midnight

"@hourly" → every hour

"@weekly" → every week

"0 12 * * *" → daily at 12 PM (cron expression)

Your example:
@daily → runs once per day at 00:00.

✅ 4. catchup

What it is:
Controls whether Airflow should run backfill for past dates.

🔹 If catchup=True:

Airflow will run all missing DAG runs from start_date to today.

🔹 If catchup=False (recommended for most cases):

Airflow will not run old backfill jobs.
It will start running only from the next scheduled interval onward.

Your example:
catchup=False → No old DAG runs will be executed.

| Parameter           | Meaning                       | Your Value     | Result                       |
| ------------------- | ----------------------------- | -------------- | ---------------------------- |
| `dag_id`            | Unique name for DAG           | `"sample_dag"` | DAG shown as `sample_dag`    |
| `start_date`        | When scheduling begins        | `2025-01-01`   | DAG first day is Jan 1, 2025 |
| `schedule_interval` | How often DAG runs            | `"@daily"`     | Runs everyday at midnight    |
| `catchup`           | Should Airflow run past dates | `False`        | No backfill                  |

Cron jobs:

Breakdown of "0 12 * * *"

| Field | Meaning      | Value             |
| ----- | ------------ | ----------------- |
| `0`   | Minute       | 0th minute        |
| `12`  | Hour         | 12 PM             |
| `*`   | Day of Month | Every day         |
| `*`   | Month        | Every month       |
| `*`   | Day of Week  | Every day of week |

🧠 Want more cron examples?

I can also explain:

"*/5 * * * *" → every 5 minutes

"0 */2 * * *" → every 2 hours

"30 6 * * 1" → every Monday at 6:30 AM

"0 0 1 * *" → first day of month at midnight
