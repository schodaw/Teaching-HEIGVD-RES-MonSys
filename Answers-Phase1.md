# Answers, Phase 1

```
Dominique Jollien
Frédéric Saam

We certify that we have done all the lab tasks and we have a running environment on our 
machine to prove it. We are ready to demonstrate it at any time and to explain the process
we have followed.
# -------------------------------
```


```
# -- YOUR ANSWER TO QUESTION 1 --

La commande vagrant up a été lancée une fois puis nous avons du redémarrer et relancer la commande. Ci-dessous ne se trouve donc que le résultat de la 2ème commande.

C:\Data\RES\GitHub\Teaching-HEIGVD-RES-MonSys\monsys-web-infra>vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
    default: Adapter 2: hostonly
==> default: Forwarding ports...
    default: 9090 => 8080 (adapter 1)
    default: 22 => 2222 (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: Warning: Connection timeout. Retrying...
    default: Warning: Connection timeout. Retrying...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Configuring and enabling network interfaces...
==> default: Mounting shared folders...
    default: /vagrant => C:/Data/RES/GitHub/Teaching-HEIGVD-RES-MonSys/monsys-web-infra
==> default: Running provisioner: shell...
    default: Running: inline script
stdin: is not a tty
Cleaning up Docker containers...
/tmp/vagrant-shell: line 2: docker: command not found
/tmp/vagrant-shell: line 3: docker: command not found
/tmp/vagrant-shell: line 4: docker: command not found
/tmp/vagrant-shell: line 5: docker: command not found
/tmp/vagrant-shell: line 6: docker: command not found
/tmp/vagrant-shell: line 7: docker: command not found
/tmp/vagrant-shell: line 8: docker: command not found
/tmp/vagrant-shell: line 9: docker: command not found
==> default: Running provisioner: docker...
    default: Installing Docker (latest) onto machine...
    default: Configuring Docker to autostart containers...
==> default: Building Docker images...
==> default: -- Path: /vagrant/docker/rp-nginx
==> default: -- Path: /vagrant/docker/web-apache
==> default: -- Path: /vagrant/docker/app-nodejs
==> default: Starting Docker containers...
==> default: -- Container: rp-node
==> default: -- Container: web-node-1
==> default: -- Container: web-node-2
==> default: -- Container: app-node

# -------------------------------
```

```
# -- YOUR ANSWER TO QUESTION 2 --

C:\Data\RES\GitHub\Teaching-HEIGVD-RES-MonSys\monsys-web-infra>vagrant ssh
Welcome to Ubuntu 14.04 LTS (GNU/Linux 3.13.0-24-generic x86_64)

 * Documentation:  https://help.ubuntu.com/
Last login: Tue Apr 22 19:47:09 2014 from 10.0.2.2
vagrant@ubuntu-14:~$ uname -a
Linux ubuntu-14 3.13.0-24-generic #46-Ubuntu SMP Thu Apr 10 19:11:08 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux

# -------------------------------
```

```
# -- YOUR ANSWER TO QUESTION 3 --

vagrant@ubuntu-14:~$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED              VIRTUAL SIZE
heig/rp-nginx       latest              76fae8956706        About a minute ago   637.9 MB
heig/app-nodejs     latest              24fd920a5954        18 minutes ago       398.9 MB
heig/web-apache     latest              0ff77a2da53c        21 minutes ago       411.9 MB
<none>              <none>              9fea7ad91b3b        25 minutes ago       637.9 MB
dockerfile/ubuntu   latest              cbc81be8f75e        12 days ago          378.6 MB

# -------------------------------
```

```
# -- YOUR ANSWER TO QUESTION 4 --

vagrant@ubuntu-14:~$ docker ps
CONTAINER ID        IMAGE                    COMMAND                CREATED             STATUS              PORTS                  NAMES
e11aab4621e6        heig/app-nodejs:latest   node /opt/server.js    20 seconds ago      Up 19 seconds       0.0.0.0:7070->80/tcp   app-node
450c696def8c        heig/web-apache:latest   /usr/sbin/apache2ctl   21 seconds ago      Up 20 seconds       0.0.0.0:8082->80/tcp   web-node-2
f4266701936e        heig/web-apache:latest   /usr/sbin/apache2ctl   21 seconds ago      Up 20 seconds       0.0.0.0:8081->80/tcp   web-node-1
58a6a03a64ab        heig/rp-nginx:latest     /opt/init.sh           22 seconds ago      Up 21 seconds       0.0.0.0:9090->80/tcp   rp-node
# -------------------------------
```

```
# -- YOUR ANSWER TO QUESTION 5 --

app-node : 172.17.0.5
web-node-2 : 172.17.0.4
web-node-1 : 172.17.0.3
rp-node : 172.17.0.2

# -------------------------------
```

```
# -- YOUR ANSWER TO QUESTION 6 --

Host (your laptop):
- IP address: 10.192.80.253

Virtual Machine run by Virtual Box
- IP address: 192.168.33.20
- PAT: packets arriving on 10.192.80.253:8080 are forwarded to 192.168.33.20:9090

Docker Bridge
- IP address: 172.17.42.1
- PAT: packets arriving on 172.17.42.1:7070 are forwarded to 172.17.0.5:80
- PAT: packets arriving on 172.17.42.1:8082 are forwarded to 172.17.0.4:80
- PAT: packets arriving on 172.17.42.1:8081 are forwarded to 172.17.0.3:80
- PAT: packets arriving on 172.17.42.1:9090 are forwarded to 172.17.0.2:80

Docker Container 1
- IP address: 172.17.0.5

Docker Container 2
- IP address: 172.17.0.4

Docker Container 3
- IP address: 172.17.0.3

Docker Container 4
- IP address: 172.17.0.2

# -------------------------------
```

```
# -- YOUR ANSWER TO QUESTION 7 --

Which command did you type on the terminal to establish the connection?
telnet 192.168.33.20 9090

What HTTP request did you type and send?
GET / HTTP/1.1
Host: www.monsys.com


What HTTP response did you get?
HTTP/1.1 200 OK
Server: nginx/1.6.0
Date: Thu, 15 May 2014 07:35:28 GMT
Content-Type: text/html
Content-Length: 1584
Connection: keep-alive
X-Powered-By: PHP/5.5.9-1ubuntu4
Vary: Accept-Encoding

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
        "http://www.w3.org/TR/html4/loose.dtd">
<html>
        <head>
                <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
                <link href='http://fonts.googleapis.com/css?family=Terminal+Dosis' rel='stylesheet' type='text/css'>
                <link href='css/main.css' rel='stylesheet' type='text/css'>
                <script type="text/javascript" src="script/jquery-1.6.4.js"></script>
                <title>Welcome To MonSys Front-End</title>

                <script language="JavaScript">

                        $(document).ready(function () {
                                refreshNodes();
                        });

                        function refreshNodes() {
                            $.getJSON('/ajax/resources/nodes',
                            function(data) {
                                var items = [];

                                $.each(data,
                                function(key, val) {
                                    items.push('<li>' + val.name + ", " + val.description + ", load: " + val.currentLoadLevel + ' %</li>');
                                });

                                $('#monitor').html("<ul>" + items.join('') + "</ul>");
                            });
                                var t=setTimeout("refreshNodes()", 1000);
                        }
        </script>
        </head>
        <body>
                <h1>Welcome to MonSys</h1>
                <h2>You are connected to the front-end system, implemented in PHP</h2>
                <b>Note</b>: this page is sending HTTP GET requests to <verbatim>/ajax/resources/nodes</verbatim> in order to retrieve JSON representations of the resources managed by the back-end.
                <p/>

                <div id="monitor">
                        You should monitoring data coming from the back-end here.
                </div>

                <br/>
                Brought to you by the University of Applied Sciences of Western Switzerland
        </body>
</html>
Connection closed by foreign host.
# -------------------------------
```

```
# -- YOUR ANSWER TO QUESTION 8 --

Which command did you type on the terminal to establish the connection?
telnet 192.168.33.20 9090

What HTTP request did you type and send?
GET /ajax/resources/nodes HTTP/1.1
Host: www.monsys.com


What HTTP response did you get?
HTTP/1.1 200 OK
Server: nginx/1.6.0
Date: Thu, 15 May 2014 07:46:50 GMT
Content-Type: application/json
Transfer-Encoding: chunked
Connection: keep-alive

fa
[{"name":"P-001","description":"Epson Printer","currentLoadLevel":74.9551200773567},{"n
HP Printer","currentLoadLevel":49.00161297991872}]
0
# -------------------------------
```

```
# -- YOUR ANSWER TO QUESTION 9 --

What procedure did you follow to validate the configuration of 
your new web nodes?
commandes utilisées :
vagrant provision
vagrant ssh
docker ps

Provide details and evidence (command results, etc.) that your 
setup is correct.

C:\Data\RES\GitHub\Teaching-HEIGVD-RES-MonSys\monsys-web-infra>vagrant provision
==> default: Running provisioner: shell...
    default: Running: inline script
stdin: is not a tty
Cleaning up Docker containers...
rp-node
web-node-1
web-node-2
app-node
clash-node-1
clash-node-2
clash-node-3
rp-node
web-node-1
web-node-2
app-node
clash-node-1
clash-node-2
clash-node-3
==> default: Running provisioner: docker...
    default: Configuring Docker to autostart containers...
==> default: Building Docker images...
==> default: -- Path: /vagrant/docker/rp-nginx
==> default: -- Path: /vagrant/docker/web-apache
==> default: -- Path: /vagrant/docker/app-nodejs
==> default: -- Path: /vagrant/docker/web-clash
==> default: Starting Docker containers...
==> default: -- Container: rp-node
==> default: -- Container: web-node-1
==> default: -- Container: web-node-2
==> default: -- Container: app-node
==> default: -- Container: clash-node-1
==> default: -- Container: clash-node-2
==> default: -- Container: clash-node-3

C:\Data\RES\GitHub\Teaching-HEIGVD-RES-MonSys\monsys-web-infra>vagrant ssh
Welcome to Ubuntu 14.04 LTS (GNU/Linux 3.13.0-24-generic x86_64)

 * Documentation:  https://help.ubuntu.com/
Last login: Mon May 19 11:59:00 2014 from 10.0.2.2
vagrant@ubuntu-14:~$ docker ps
CONTAINER ID        IMAGE                    COMMAND                CREATED             STATUS
        PORTS                  NAMES
7e774bd4a226        heig/web-clash:latest    /usr/sbin/apache2ctl   38 seconds ago      Up 38 seconds 0.0.0.0:8085->80/tcp   clash-node-3
89cb98d66f44        heig/web-clash:latest    /usr/sbin/apache2ctl   39 seconds ago      Up 39 seconds       0.0.0.0:8084->80/tcp   clash-node-2
7ff746ff88a5        heig/web-clash:latest    /usr/sbin/apache2ctl   40 seconds ago      Up 39 seconds       0.0.0.0:8083->80/tcp   clash-node-1
1744b78d6216        heig/app-nodejs:latest   node /opt/server.js    40 seconds ago      Up 40 seconds       0.0.0.0:7070->80/tcp   app-node
4da278f3fb07        heig/web-apache:latest   /usr/sbin/apache2ctl   41 seconds ago      Up 41 seconds       0.0.0.0:8082->80/tcp   web-node-2
fbc7d4efedf1        heig/web-apache:latest   /usr/sbin/apache2ctl   42 seconds ago      Up 41 seconds       0.0.0.0:8081->80/tcp   web-node-1
7eae7b4a3edd        heig/rp-nginx:latest     /opt/init.sh           42 seconds ago      Up 42 seconds       0.0.0.0:9090->80/tcp   rp-node


C:\Users\admin>telnet 192.168.33.20 8083
Trying 192.168.33.20...
Connected to 192.168.33.20.
Escape character is '^]'.
GET / HTTP/1.1
Host: live.clashofclasses.ch

HTTP/1.1 200 OK
Date: Mon, 19 May 2014 12:19:08 GMT
Server: Apache/2.4.7 (Ubuntu)
Last-Modified: Thu, 15 May 2014 07:08:35 GMT
ETag: "80a-4f96af723a2c0"
Accept-Ranges: bytes
Content-Length: 2058
Vary: Accept-Encoding
Content-Type: text/html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="">
    <meta name="author" content="">
        <link href="http://netdna.bootstrapcdn.com/font-awesome/4.0.3/css/font-awesome.css" rel="sty
lesheet">
    <title>Sticky Footer Template for Bootstrap</title>

    <!-- Bootstrap core CSS -->
    <link href="./css/live-bootstrap.css" rel="stylesheet">

    <!-- Custom styles for this template -->
    <link href="./css/sticky-footer.css" rel="stylesheet">

    <!-- Just for debugging purposes. Don't actually copy this line! -->
    <!--[if lt IE 9]><script src="../../assets/js/ie8-responsive-file-warning.js"></script><![endif]
-->

    <!-- HTML5 shim and Respond.js IE8 support of HTML5 elements and media queries -->
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
      <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>

  <body>

    <!-- Begin page content -->
    <div class="container">
      <div class="page-header">
        <h1>Welcome To Clash of Classes!</h1>
      </div>
...


C:\Users\admin>telnet 192.168.33.20 8083
Trying 192.168.33.20...
Connected to 192.168.33.20.
Escape character is '^]'.
GET / HTTP/1.1
Host: dashboard.clashofclasses.ch

HTTP/1.1 200 OK
Date: Mon, 19 May 2014 12:19:50 GMT
Server: Apache/2.4.7 (Ubuntu)
Last-Modified: Thu, 15 May 2014 07:08:35 GMT
ETag: "809-4f96af723a2c0"
Accept-Ranges: bytes
Content-Length: 2057
Vary: Accept-Encoding
Content-Type: text/html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="">
    <meta name="author" content="">
        <link href="http://netdna.bootstrapcdn.com/font-awesome/4.0.3/css/font-awesome.css" rel="sty
lesheet">
    <title>Sticky Footer Template for Bootstrap</title>

    <!-- Bootstrap core CSS -->
    <link href="./css/dashboard-bootstrap.css" rel="stylesheet">

    <!-- Custom styles for this template -->
    <link href="./css/sticky-footer.css" rel="stylesheet">

    <!-- Just for debugging purposes. Don't actually copy this line! -->
    <!--[if lt IE 9]><script src="../../assets/js/ie8-responsive-file-warning.js"></script><![endif]
-->

    <!-- HTML5 shim and Respond.js IE8 support of HTML5 elements and media queries -->
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
      <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>

  <body>

    <!-- Begin page content -->
    <div class="container">
      <div class="page-header">
        <h1>Clash of Classes Dashboard</h1>
      </div>
...
# -------------------------------
```

```
# -- YOUR ANSWER TO QUESTION 10 --

What procedure did you follow to validate the configuration of 
your complete infrastructure?
Commandes utilisées : docker ps, telnet
ouvrir la page http://live.clashofclasses.ch/ avec un browser
ouvrir la page http://dashboard.clashofclasses.ch/ avec un browser

Provide details and evidence (command results, etc.) that your 
setup is correct.

docker ps  :
vagrant@ubuntu-14:~$ docker ps
CONTAINER ID        IMAGE                    COMMAND                CREATED             STATUS
        PORTS                  NAMES
f17772d0108c        heig/web-clash:latest    /usr/sbin/apache2ctl   16 minutes ago      Up 16 minutes       0.0.0.0:8085->80/tcp   clash-node-3
41dc595f19d4        heig/web-clash:latest    /usr/sbin/apache2ctl   16 minutes ago      Up 16 minutes       0.0.0.0:8084->80/tcp   clash-node-2
9e40a74dfc67        heig/web-clash:latest    /usr/sbin/apache2ctl   16 minutes ago      Up 16 minutes       0.0.0.0:8083->80/tcp   clash-node-1
cc924d7010c5        heig/app-nodejs:latest   node /opt/server.js    16 minutes ago      Up 16 minutes       0.0.0.0:7070->80/tcp   app-node
6a484813e7cf        heig/web-apache:latest   /usr/sbin/apache2ctl   16 minutes ago      Up 16 minutes       0.0.0.0:8082->80/tcp   web-node-2
11e5fa41b59d        heig/web-apache:latest   /usr/sbin/apache2ctl   16 minutes ago      Up 16 minutes       0.0.0.0:8081->80/tcp   web-node-1
93612732559e        heig/rp-nginx:latest     /opt/init.sh           16 minutes ago      Up 16 minutes       0.0.0.0:80->80/tcp     rp-node

telnet :
C:\Users\admin>telnet live.clashofclasses.ch 80
Trying 192.168.33.20...
Connected to live.clashofclasses.ch.
Escape character is '^]'.
GET / HTTP/1.1
Host: live.clashofclasses.ch

HTTP/1.1 200 OK
Server: nginx/1.6.0
Date: Thu, 22 May 2014 07:22:19 GMT
Content-Type: text/html
Content-Length: 2058
Connection: keep-alive
Last-Modified: Thu, 15 May 2014 07:08:35 GMT
ETag: "80a-4f96af723a2c0"
Accept-Ranges: bytes
Vary: Accept-Encoding

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="">
    <meta name="author" content="">
        <link href="http://netdna.bootstrapcdn.com/font-awesome/4.0.3/css/font-awesome.css" rel="sty
lesheet">
    <title>Sticky Footer Template for Bootstrap</title>

    <!-- Bootstrap core CSS -->
    <link href="./css/live-bootstrap.css" rel="stylesheet">

    <!-- Custom styles for this template -->
    <link href="./css/sticky-footer.css" rel="stylesheet">

    <!-- Just for debugging purposes. Don't actually copy this line! -->
    <!--[if lt IE 9]><script src="../../assets/js/ie8-responsive-file-warning.js"></script><![endif]
-->

    <!-- HTML5 shim and Respond.js IE8 support of HTML5 elements and media queries -->
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
      <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>

  <body>

    <!-- Begin page content -->
    <div class="container">
      <div class="page-header">
        <h1>Welcome To Clash of Classes!</h1>
      </div>
......

C:\Users\admin>telnet dashboard.clashofclasses.ch 80
Trying 192.168.33.20...
Connected to dashboard.clashofclasses.ch.
Escape character is '^]'.
GET / HTTP/1.1
Host: dashboard.clashofclasses.ch

HTTP/1.1 200 OK
Server: nginx/1.6.0
Date: Thu, 22 May 2014 07:24:58 GMT
Content-Type: text/html
Content-Length: 2057
Connection: keep-alive
Last-Modified: Thu, 15 May 2014 07:08:35 GMT
ETag: "809-4f96af723a2c0"
Accept-Ranges: bytes
Vary: Accept-Encoding

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="">
    <meta name="author" content="">
        <link href="http://netdna.bootstrapcdn.com/font-awesome/4.0.3/css/font-awesome.css" rel="sty
lesheet">
    <title>Sticky Footer Template for Bootstrap</title>

    <!-- Bootstrap core CSS -->
    <link href="./css/dashboard-bootstrap.css" rel="stylesheet">

    <!-- Custom styles for this template -->
    <link href="./css/sticky-footer.css" rel="stylesheet">

    <!-- Just for debugging purposes. Don't actually copy this line! -->
    <!--[if lt IE 9]><script src="../../assets/js/ie8-responsive-file-warning.js"></script><![endif]
-->

    <!-- HTML5 shim and Respond.js IE8 support of HTML5 elements and media queries -->
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
      <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>

  <body>

    <!-- Begin page content -->
    <div class="container">
      <div class="page-header">
        <h1>Clash of Classes Dashboard</h1>
      </div>
.......
# -------------------------------
```

