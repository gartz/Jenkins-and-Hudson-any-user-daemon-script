Jernins and Hudson any user dameon script
=========================================

[![Analytics](https://ga-beacon.appspot.com/UA-24619548-7/Jenkins-and-Hudson-any-user-daemon-script/readme)](https://github.com/igrigorik/ga-beacon)

It's the simplest way to any linux start and stop the Jerskins or Hudson .war file in a single bash user from a server. It will ran in background mode silent, and generate a log file to keep tracking the output.

### About CI:

* [Jenkins](http://jenkins-ci.org/) -- Fork from the original team after Oracle buy Sun.
* [Hudson](http://hudson-ci.org/) -- Original project maintained by Oracle as free (for how long?)
* [Wikipedia](http://en.wikipedia.org/wiki/Continuous_integration) -- Just if you don't know why are you here...

This script will work with both, actualy I'm a jenkins lover, but I started to use it before the project fork. So keep to your self the responsability of choice.

How to install
--------------

1. Download Hudson or Jenkins to a folder (you can use the built-in project .war file if you want)
2. Move the `bin/hudsond` folder to your `$HOME/bin/hudsond`
3. Use [vi](http://en.wikipedia.org/wiki/Vi) or [nano](http://en.wikipedia.org/wiki/Nano_%28text_editor%29) to edit `hudsond` configs.

You can rename `hudson.jar` to `jenkins.jar` and/or `hudsond` to `jenkinsd` as you wan't, but don't forget to edit the configs.

Create a folder .hudson in your user home with privileges to user can read/write/exec

~~~
cd ~/
mkdir .hudson
chown $USER .hudosn
chmod 0750 .hudson
~~~

Add execute privileges to `hudsond`

~~~
cd $HOME/bin
chmod +x ./hudsond
~~~

Configuration
-------------

Simple like sugar, open you hudsond.

~~~
DESC="Hudson CI Server"
HUDSON_FOLDER=${HOME}/hudson
HUDSON_WAR=hudson.war
HUDSON_LOG=${HUDSON_FOLDER}/hudson.log
JAVA=/usr/bin/java
PORT=9080
ADDR=127.0.0.1
HUDSON_ADMIN_USER=admin
~~~

Starting Hudson
---------------

When you type:

~~~
cd $HOME/bin
./hudsond start
~~~

It will start as background, so you can close you tty if you want. And will be accessible in ADD and PORT you setup.

Like `http://127.0.0.1:9080`

I recomend you do a reverse proxy to the internal address with a custom config from [apache2][ref-apache2] or [nginx][ref-nginx]

You also can configure to use HTTPS in the proxy-reverse, but don't forget to configure in the hudson/jenkins options setup. Or it will advice you anyway.

### Descriptions

`DESC`: A description of the daemon
`HUDSON_FOLDER`: The folder were exec package of hudson or jenkins are found
`HUDSON_WAR`: The file name of exec package of hudson or jenkins
`HUDSON_LOG`: File where the logs will be storage.
`JAVA`: Java executable
`PORT`: Port to access by HTTP protocol
`ADDR`: Address to access the server, you can use * for any IP
`HUDSON_ADMIN_USER`: The user that have super privileges

### Other useful commands

Assuming you are inside the `bin/` folder...

Type only `./hudsond` to display help commands.


See status from hudson daemon:

    ./hudsond status


Stop you user daemon:

    ./hudosnd stop


### Updating Jenkins or Hudson

After you mark your server to secury restart in the application, now you can use the `hudsond` to restart your application simple like:

~~~
./hudsond restart
~~~

### Root commands

Stop all hudosn instances running in your server:

    ./hudosnd stop_all

Atention: you need to have `su` privileges, or use `sudo ./hudosnd stop_all`


Extra Tips
----------

Some tips to help you improve the usability of the hudson daemon script.

### Exec Path

You can put the `hudsond` file inside your `$HOME\bin` folder or add to `$PATH` to execute directly like `hudsond start` without `./` prefix.

Edit your `.bash_profile` last line:

    PATH=$PATH:$HOME/bin

### Reading logs

Display log on screen:

    cat hudson.log

Display real-time log:

    tail -f hudson.log

License
-------

Copyright 2011 Gabriel Reitz Giannattasio. All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are
permitted provided that the following conditions are met:

   1. Redistributions of source code must retain the above copyright notice, this list of
      conditions and the following disclaimer.

   2. Redistributions in binary form must reproduce the above copyright notice, this list
      of conditions and the following disclaimer in the documentation and/or other materials
      provided with the distribution.

THIS SOFTWARE IS PROVIDED BY GABRIEL REITZ GIANNATTASIO ``AS IS'' AND ANY EXPRESS OR IMPLIED
WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND
FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL GABRIEL REITZ GIANNATTASIO OR
CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON
ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF
ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

The views and conclusions contained in the software and documentation are those of the
authors and should not be interpreted as representing official policies, either expressed
or implied, of Gabriel Reitz Giannattasio.


[ref-apache2]: http://httpd.apache.org/
[ref-nginx]: http://nginx.net/
