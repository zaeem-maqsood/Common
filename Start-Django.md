# Common
Just some common code snippets that come in handy for Django/Python dev


# ----------------------------------------------- Create a Local & Blank Django Project

A guide for creating a Django project for use in both Local & Production (deployment) environments.
---------


1. Create Dev Directory for General Project Storage
    ```
    cd ~/
    mkdir Project && cd Project
    ```

2. Create Virtual Environment
    ```
    cd ~/Project
    mkdir ProjectName && cd ProjectName
    virtualenv -p python3 .

    # activate
    source bin/activate
    ```

3. Install Django & Start Project
    ```
    pip install django==1.10.3

    mkdir src && cd src 

    django-admin.py startproject myProjectName . 
    ```

5. Some other common installations (optional):
    ```
    # for a postgresql database
    pip install psycopg2

    # for a mysql database
    pip install MySQL-python

    # for use on heroku
    pip install gunicorn dj-database-url

    pip install django-crispy-forms
    pip install pillow
    ```

6. Create `requirements.txt` file
    ```
    pip freeze > requirements.txt
    ```

7. Run Migration & Createsuperuser
    ```
    python manage.py migrate
    python manage.py createsuperuser
    ```
