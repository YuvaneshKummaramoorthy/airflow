## Apache Airflow Setup (PyPI Installation)

#### Step 1:

Update and Upgrade Ubuntu.
```bash
sudo apt update -y
sudo apt upgrade -y
# install python3-venv to create python virtual environment
sudo apt install python3-venv -y
```

#### Step 2:
Create a python environment and upgrade the pip.
```bash
# create a directory.
mkdir airflow
# go to the directory.
cd airflow
# create a python virtual environment (airflow-env).
python3 -m venv airflow-env
# activate the virtual environment.
source airflow-env/bin/activate
# upgrade pip, setuptools and flask_appbuilder packages.
pip install --upgrade setuptools pip flask_appbuilder
```

#### Step 3:
Install apache-airflow package.
```bash
# install apache-airflow
pip install apache-airflow 
# install apache-airflow-providers-fab -> this is for creating user
pip install apache-airflow-providers-fab
```

#### Step 4:
Create the airflow configuration file.
```bash
# Set up the environment variable.
export AIRFLOW_HOME=$(pwd)
# Create the airflow configuration file.
airflow config list --defaults > "${AIRFLOW_HOME}/airflow.cfg"
```

#### Step 5:
Update following configurations.
```bash
# Update executtor to be LocalExecutor as default is sequentialExecutor.
executor = LocalExecutor
# Add auth manager if you want to create a user using airflow users.
auth_manager = airflow.providers.fab.auth_manager.fab_auth_manager.FabAuthManager
```

#### Step 6:
Create two secret keys using following.
```bash
# generate two tokens.
# one for jwt_secret:
python -c "import secrets; print(secrets.token_urlsafe(32))"
# one for secret_key:
python -c "import secrets; print(secrets.token_urlsafe(32))"
```

#### Step 7:
Update the token in the config file.
```bash
#Update jwt_secret in config file.
jwt_secret = {YOUR JWT SECRET}
# update secret_key in config file.
secret_key = {YOUR JWT SECRET}
```

#### Step 8:
Airflow db migrate
```bash
airflow db migrate
```

### Step 9:
Create a user (Admin)
```bash
airflow users create \
    --username YuvaneshKummaramoorthy \
    --firstname Yuvanesh \
    --lastname Kummaramoorthy \
    --role Admin \
    --email yuvanesh.kummaramoorthy@gmail.com
```

#### Step 10:
Launch the Airflow UI
```bash
airflow api-server --port 8080
```
