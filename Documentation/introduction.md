## Apache Airflow
Apache Airflow is an open-source platform used to create, schedule, and manage workflows (often called DAGs—Directed Acyclic Graphs). It’s commonly used for data engineering, ETL/ELT processes, machine-learning pipelines, and other tasks that need automation

A tool that runs your Python jobs, ETL jobs, and data workflows on a schedule, with full visibility and control

**Key points:**

    1. Workflow as code: You define workflows in Python, making them version-controlled, testable, and flexible.
    2. DAGs (Directed Acyclic Graphs): A workflow is expressed as tasks with upstream/downstream dependencies.
    3. Scheduler: Airflow schedules your tasks based on defined intervals or triggers.
    4. Executor: Runs tasks on different backends (Local, Celery, Kubernetes, etc.).
    5. UI: A web interface to monitor, trigger, and debug workflows.
    6. Extensibility: Large ecosystem of operators and hooks for systems like AWS, GCP, databases, Spark, etc.


**Why Airflow?**

    1. I need this script to run at 3 AM every day.
    2. Task B should run only after Task A is finished.
    3. I want retries, alerts, logging.
    4. I want a UI to see what’s running, failed, succeeded.

**Airflow is widely used in:**

    1. Data Engineering
    2. ML Pipelines
    3. ETL/ELT
    4. Analytics Workflow
    5. Cloud Automation etc...

**Key Concepts:**

    1. DAG (Directed Acyclic Graph)
        A Python file that defines:
            - tasks
            - dependencies
            - schedule

    2. Task
        A single step in your workflow.

    3. Operator
        A pre-built template for a task:
            - PythonOperator
            - BashOperator
            - EmailOperator
            - SQL operators
            - Sensor (waits for something)

    4. Scheduler
        Watches the schedule and triggers DAG runs.

    5. Executor
        Determines how tasks run
            - LocalExecutor
            - CeleryExecutor
            - KubernetesExecutor

    6. Airflow UI
        Dashboard to see DAGs, logs, task runs.


**Example:**

This defines a DAG with two tasks:
```python
# install necessary libraries:
from airflow import DAG
from airflow.operators.bash import BashOperator
from datetime import datetime

# define the dag:
with DAG(
    dag_id="example_dag",
    start_date=datetime(2024, 1, 1),
    schedule="@daily"
):
    task1 = BashOperator(
        task_id="say_hello",
        bash_command="echo hello"
    )

    task2 = BashOperator(
        task_id="say_bye",
        bash_command="echo bye"
    )

    task1 >> task2  # dependency

```