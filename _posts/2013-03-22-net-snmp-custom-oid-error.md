---
layout: post
title: "net snmp custom OID error"
description: ""
category: "monitor"
tags: [cacti,net-snmp]
---
{% include JB/setup %}



<p>用rpm包安装的net-snmp，按照配置文件自定义OID，使用snmpwalk抓取会报</p>
<pre><code>
  "UCD-SNMP-MIB::ucdavis.1 = No Such Object available on this agent at this OID"
</code></pre>

<p>解决办法：</p>
<p>将 exec 改为 extend</p> 
