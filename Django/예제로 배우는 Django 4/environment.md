# Versions
- python=3.12.10
- Django=4.2.27

## reference
[Django-python](https://docs.djangoproject.com/en/6.0/faq/install/#faq-python-version-support, "support versions")

## used command
- print availble version\
`pip index versions django`
- install newest selected version\
`pip install django~=4.2.0`
- installed version check\
`python -m django --version`
- create sample project\
`django-admin startproject <name>`
- migrate\
`cd mysite`\
`python manage.py migrate`
- run develop server\
`python manage.py runserver`\
or `python manage.py runserver 127.0.0.1:8000 --settings=mysite.settings`
- 