# Versions
- python=3.10.11
- Django=4.2.27

# VS Code
- .md preview (Ctrl+Shift+V)

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

---
## troubleshooting
### Error: You don't have permission to access that port.
> 포트 상태 조회 \
`netstat -aon | findstr :<Port>` 
>> netstat 옵션 \
-a : 연결과 대기 중인 포트 표시 \
-o : 프로세스ID(PID) 출력 \
-n : 주소와 포트를 숫자 형태로 출력 \
findstr : 필터

> 프로세스 종료 \
`taskkill /PID <PID> /F`


### test
> test


