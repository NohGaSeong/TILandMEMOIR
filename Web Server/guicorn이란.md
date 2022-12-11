# Guicorn이란?
python wsgi 로 web server 로부터 서버사이드 요청을 받으면 wsgi를 통해 서버 애플리케이션으로 전달해주는 역할을 수행한다. django의 runserver 명령어도 똑같은 역할을 수행해주지만 보안, 성능적으로 검증이 되지 않아서 배포 환경에선 쓰지 않는게 맞다. 

## production 환경에 적합함
wsgi는 멀티 쓰레드를 만들 수 있기에 request 요청이 많아지더라도 효율적으로 처리할 수 있다. 즉, production 환경에 적합하다.

## 정리
웹서버와 django 사이에서 request를 처리해주는 역할을 한다. 이 과정에서 wsgi를 사용하게 되는데 파이썬에서 대표적인 wsgi는 uWSGI, gunicorn이 존재한다. 두개중 gunicorn의 퍼모먼스가 조금 더 좋고 가볍다는 의견이 대다수이기에 많은 사람들이 gunicorn을 사용한다고한다. (필자도 이거 사용함)
