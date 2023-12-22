```bash
+ umask 022

+ cd /root/rpmbuild/BUILD

+ cd nginx-1.20.2

+ /usr/bin/rm -rf /root/rpmbuild/BUILDROOT/nginx-1.20.2-1.el8.ngx.x86_64

+ exit 0

[root@centos8s ~]# ll rpmbuild/RPMS/x86_64/

total 4456

-rw-r--r--. 1 root root 2061068 Dec 22 13:41 nginx-1.20.2-1.el8.ngx.x86_64.rpm

-rw-r--r--. 1 root root 2495748 Dec 22 13:41 nginx-debuginfo-1.20.2-1.el8.ngx.x86_64.rpm

[root@centos8s ~]# systemctl start nginx

[root@centos8s ~]# systemctl status nginx

● nginx.service - nginx - high performance web server

   Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled; vendor preset: disabled)

   Active: active (running) since Fri 2023-12-22 13:47:55 UTC; 6s ago

     Docs: http://nginx.org/en/docs/

  Process: 24191 ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx.conf (code=exited, status=0/SUCCESS)

 Main PID: 24192 (nginx)

    Tasks: 3 (limit: 11145)

   Memory: 2.9M

   CGroup: /system.slice/nginx.service

           ├─24192 nginx: master process /usr/sbin/nginx -c /etc/nginx/nginx.conf

           ├─24193 nginx: worker process

           └─24194 nginx: worker process



Dec 22 13:47:55 centos8s.localdomain systemd[1]: Starting nginx - high performance web server...

Dec 22 13:47:55 centos8s.localdomain systemd[1]: Started nginx - high performance web server.

[root@centos8s ~]# createrepo /usr/share/nginx/html/repo/

Directory walk started

Directory walk done - 2 packages

Temporary output repo path: /usr/share/nginx/html/repo/.repodata/

Preparing sqlite DBs

Pool started (with 5 workers)

Pool finished

[root@centos8s ~]# ls /usr/share/nginx/html/repo/

nginx-1.20.2-1.el8.ngx.x86_64.rpm  percona-  percona-orchestrator-3.2.6-2.el8.x86_64.rpm  repodata

[root@centos8s ~]# curl -a http://localhost/repo/

<html>

<head><title>Index of /repo/</title></head>

<body>

<h1>Index of /repo/</h1><hr><pre><a href="../">../</a>

<a href="repodata/">repodata/</a>                                          22-Dec-2023 14:02                   -

<a href="nginx-1.20.2-1.el8.ngx.x86_64.rpm">nginx-1.20.2-1.el8.ngx.x86_64.rpm</a>                  22-Dec-2023 13:50             2061068

<a href="percona-">percona-</a>                                           16-Feb-2022 15:57             5222976

<a href="percona-orchestrator-3.2.6-2.el8.x86_64.rpm">percona-orchestrator-3.2.6-2.el8.x86_64.rpm</a>        16-Feb-2022 15:57             5222976

</pre><hr></body>

</html>

[root@centos8s ~]# yum repolist enabled | grep otus

Failed to set locale, defaulting to C.UTF-8

otus                otus-linux

[root@centos8s ~]# yum install percona-orchestrator.x86_64 -y

Failed to set locale, defaulting to C.UTF-8

CentOS Stream 8 - AppStream                                                                                                                                                                                                                               2.2 kB/s | 4.4 kB     00:01    

CentOS Stream 8 - BaseOS                                                                                                                                                                                                                                  2.4 kB/s | 3.9 kB     00:01    

CentOS Stream 8 - Extras                                                                                                                                                                                                                                  1.5 kB/s | 2.9 kB     00:01    

CentOS Stream 8 - Extras common packages                                                                                                                                                                                                                  1.5 kB/s | 3.0 kB     00:02    

Extra Packages for Enterprise Linux 8 - x86_64                                                                                                                                                                                                            5.6 kB/s | 7.6 kB     00:01    

Extra Packages for Enterprise Linux 8 - Next - x86_64                                                                                                                                                                                                     6.1 kB/s | 9.4 kB     00:01    

otus-linux                                                                                                                                                                                                                                                122 kB/s | 2.8 kB     00:00    

Dependencies resolved.

==========================================================================================================================================================================================================================================================================================

 Package                                                                     Architecture                                                  Version                                                                 Repository                                                        Size

==========================================================================================================================================================================================================================================================================================

Installing:

 percona-orchestrator                                                        x86_64                                                        2:3.2.6-2.el8                                                           otus                                                             5.0 M

Installing dependencies:

 jq                                                                          x86_64                                                        1.6-8.el8                                                               appstream                                                        203 k

 oniguruma                                                                   x86_64                                                        6.8.2-2.el8                                                             appstream                                                        187 k



Transaction Summary

==========================================================================================================================================================================================================================================================================================

Install  3 Packages



Total download size: 5.4 M

Installed size: 17 M

Downloading Packages:

(1/3): percona-orchestrator-3.2.6-2.el8.x86_64.rpm                                                                                                                                                                                                         80 MB/s | 5.0 MB     00:00    

(2/3): jq-1.6-8.el8.x86_64.rpm                                                                                                                                                                                                                            194 kB/s | 203 kB     00:01    

(3/3): oniguruma-6.8.2-2.el8.x86_64.rpm                                                                                                                                                                                                                   168 kB/s | 187 kB     00:01    

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Total                                                                                                                                                                                                                                                     2.7 MB/s | 5.4 MB     00:01     

Running transaction check

Transaction check succeeded.

Running transaction test

Transaction test succeeded.

Running transaction

  Preparing        :                                                                                                                                                                                                                                                                  1/1 

  Installing       : oniguruma-6.8.2-2.el8.x86_64                                                                                                                                                                                                                                     1/3 

  Running scriptlet: oniguruma-6.8.2-2.el8.x86_64                                                                                                                                                                                                                                     1/3 

  Installing       : jq-1.6-8.el8.x86_64                                                                                                                                                                                                                                              2/3 

  Installing       : percona-orchestrator-2:3.2.6-2.el8.x86_64                                                                                                                                                                                                                        3/3 

  Running scriptlet: percona-orchestrator-2:3.2.6-2.el8.x86_64                                                                                                                                                                                                                        3/3 

  Verifying        : jq-1.6-8.el8.x86_64                                                                                                                                                                                                                                              1/3 

  Verifying        : oniguruma-6.8.2-2.el8.x86_64                                                                                                                                                                                                                                     2/3 

  Verifying        : percona-orchestrator-2:3.2.6-2.el8.x86_64                                                                                                                                                                                                                        3/3 



Installed:

  jq-1.6-8.el8.x86_64                                                                oniguruma-6.8.2-2.el8.x86_64                                                                percona-orchestrator-2:3.2.6-2.el8.x86_64                                                               



Complete!

```






