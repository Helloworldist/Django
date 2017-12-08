# **개선점 1**

일단 Django의 한글문서 자체가 풍부한 편이 아니라 이 문서를 작성하였습니다.


만약 window hostname이 한글일 때, ```$ python manage.py runserver``` 명령을 실행 시키면 이런 아래의 에러가 나옵니다. 

~~~~
System check identified no issues (0 silenced).

You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.
May 31, 2016 - 16:38:57
Django version 1.9.6, using settings 'untitled1.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.
Unhandled exception in thread started by .wrapper at 0x036C56A8>
Traceback (most recent call last):
File "C:\Program Files (x86)\Python35-32\lib\site-packages\django\utils\autoreload.py", line 226, in wrapper
fn(*args, **kwargs)
File "C:\Program Files (x86)\Python35-32\lib\site-packages\django\core\management\commands\runserver.py", line 137, in inner_run
ipv6=self.use_ipv6, threading=threading)
File "C:\Program Files (x86)\Python35-32\lib\site-packages\django\core\servers\basehttp.py", line 188, in run
httpd = httpd_cls(server_address, WSGIRequestHandler, ipv6=ipv6)
File "C:\Program Files (x86)\Python35-32\lib\site-packages\django\core\servers\basehttp.py", line 73, in init
super(WSGIServer, self).init(*args, **kwargs)
File "C:\Program Files (x86)\Python35-32\lib\socketserver.py", line 443, in init
self.server_bind()
File "C:\Program Files (x86)\Python35-32\lib\site-packages\django\core\servers\basehttp.py", line 77, in server_bind
super(WSGIServer, self).server_bind()
File "C:\Program Files (x86)\Python35-32\lib\wsgiref\simple_server.py", line 50, in server_bind
HTTPServer.server_bind(self)
File "C:\Program Files (x86)\Python35-32\lib\http\server.py", line 140, in server_bind
self.server_name = socket.getfqdn(host)
File "C:\Program Files (x86)\Python35-32\lib\socket.py", line 662, in getfqdn
hostname, aliases, ipaddrs = gethostbyaddr(name)
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xc0 in position 0: invalid start byte
~~~~

이러한 에러는 마지막 줄에 볼 수 있듯이 유니코드를 디코드할 때 해석할 수 없어서 발생하는 에러입니다.  
이를 해결하기 위해서는...  
cmd창 관리자 권한으로 실행해서 다음 명령어를 실행해줍니다. 

~~~
wmic ComputerSystem Where Name="%COMPUTERNAME%" Call Rename Name="원하는 호스트명(단, 무조건 영어로)"
~~~~

그리고 재부팅하면 해결 될 것입니다.  
아무래도 해외에서 주로 사용하는 오픈소스들은 한글 인코딩문제가 심심치 않게 발생합니다.  
따라서 한국어 뿐만 아니라 다국어들에 대해서도 많은 언어적 지원이 되어 이용에 차질이 없도록 이러한 점을 개선시켰으면 합니다.
