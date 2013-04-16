---
layout: post
title: "python绘图模块matplotlib"
description: ""
category: "python"
tags: [python,matplotlib]
---
{% include JB/setup %}

最近需要对数据做展示，搜了一下matplotlib是python一个非常强大的绘图模块。</br>

###一、安装模块###
<pre><code>
$ sudo apt-get install python_numpy python_matplotlib
</pre></code>

###二、语法###
<pre><code>

import numpy as np
import matplotlib.pyplot as plt
import random

x = np.linspace(0, 1440, 1440)      # 0-1440取1440个点
list = range(0,1440)                # 取0-59列表
y = random.sample(list, 1440)       # 从list中随机获取40个元素
t = ['00:00', '01:00', '02:00', '03:00', '04:00', '05:00', '06:00', '07:00', '08:00', '09:00', '10:00', '11:00', '12:00', '13:00', '14:00', '15:00', '16:00', '17:00', '18:00', '19:00', '20:00', '21:00', '22:00', '23:00', '00:00']

fig = plt.figure(figsize=(8,4))     # 指定绘图对象的宽度和高度
plt.plot(x,y,'ro-',label="test",color="red",linewidth=1)    # label=曲线名字，color=颜色，linewidth=曲线宽度。
plt.xlabel("xlabel")                # 设置x轴标签
plt.ylabel("ylabel")                # 设置y轴标签
plt.title("title")                  # 设置标题
plt.xlim(0,144)                     # x轴范围
plt.ylim(0,1500)                    # y轴范围

xmajorLocator   = plt.MultipleLocator(6)    #将x主刻度标签设置为5的倍数
ymajorLocator   = plt.MultipleLocator(100)  #将y轴主刻度标签设置为5的倍数

ax = plt.gca()
ax.set_xticklabels( t )             # 设置x轴标签，用t的值代替x轴标签

#设置主刻度标签的位置,标签文本的格式
ax.xaxis.set_major_locator(xmajorLocator)
ax.yaxis.set_major_locator(ymajorLocator)

#显示次刻度标签的位置,没有标签文本
ax.xaxis.set_minor_locator(xminorLocator)
ax.yaxis.set_minor_locator(yminorLocator)

fig.autofmt_xdate()                 # 定义x格式，如果拥挤倾斜显示
plt.grid(True)                      # 显示网格
plt.legend()                        # 显示图例
plt.show()

</pre></code>