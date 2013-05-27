---
layout: post
title: "nginx+php-cgi timeout详解"
description: ""
category: "web"
tags: [web,nginx,php]
---
{% include JB/setup %}


###前言###
   公司用的是nginx+php-cgi的架构，程序员写程序喜欢先打开数据库，最后一起关闭，这样就造成中间某个环节出问题，数据的链接数直接彪的很高，mysql用"show processlist" 查看链接全是"Sleep"状态。慢慢的将整个网站拖死。做为苦逼的运维，在应用上解决这个问题就是在服务上加上timeout超时设置，杀掉超时的php.
nginx有3个关于fastcgi timeout的配置，php.ini里有1个，php-fpm.conf里有一个。

###一、超时参数###
####1、nginx####
指定连接到后端FastCGI的超时时间。</br>
fastcgi_connect_timeout:	</br>

指定向FastCGI传送请求的超时时间，这个值是已经完成两次握手后向FastCGI传送请求的超时时间。</br>
fastcgi_send_timeout:</br>

指定接收FastCGI应答的超时时间，这个值是已经完成两次握手后接收FastCGI应答的超时时间。	</br>
fastcgi_read_timeout:</br>	


####2、php.ini####
php脚本最大执行时间</br>
max_execution_time = 60 </br>

####3、php-fpm.conf####
在单个请求等待执行时间限制</br>
request_terminate_timeout</br>


###二、测试###
1、写一个php,写一个链接数据库的sql,让它100秒执行完毕sleep(100),然后再关闭和数据库的链接。</br>
2、调整几个参数。</br>
3、数据库用"show processlist"查看链接状态，</br>
4、观察nginx日志，看看访问状态。</br>


###三、测试结果###
1、调整nginx.conf的3个参数，参数生效，日志状态504,mysql的链接状态还是sleep。</br>
2、调整php.ini的参数，参数不生效，php脚本不会中断，mysql链接状态还是sleep.</br>
3、调整php-fpm.conf, 参数生效，日志状态502,mysql的链接状态无链接。</br>

总结：从测试结果来看，修改php-fpm.conf的"request_terminate_timeout"，达到我们需要的效果。</br>

顺便说一下，php-fpm.conf还有2个参数，是把php里超过设定时间的脚本打印处理，并显示超时的php函数，方便运维排查问题。</br>
设置php脚本的超时时间，将结果记录到slowlog里。</br>
\<value name="request_slowlog_timeout">10s</value></br>
设置slowlog的日志位置。</br>
\<value name="slowlog">/var/log/slow.log</value></br>


---
















