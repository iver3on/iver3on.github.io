---
layout: post
title:  "win10��docker����java web����+����windows10Ŀ¼+����Ӧ��"
date:   2016-06-30 11:06:05
categories: docker ΢���� �ֲ�ʽ linux tomcat
tags: docker ΢���� �ֲ�ʽ linux tomcat
---

* content
{:toc}

�ܽ���win10��docker����java web����+����windows10Ŀ¼+����Ӧ��





<h1>���𻷾�</h1>
windows��������docker��������java web������

һ��������Ҫ�Լ���дdockerfile�ļ����������棺
<blockquote>FROM dordoka/tomcat
MAINTAINER iver3on &lt;grepzwb@qq.com&gt;
ENV REFRESHED_AT 2016-6-28
EXPOSE 8080 9000</blockquote>
����docker�ٷ��������ṩ��̫���˿�Դ���񣬱���tomcat mysql jdk redis ruby �ȡ��������ǿ���ֱ��pull���ɡ�

������ֱ�Ӵ�Docker Quickstart Terminal����½docker��

�������Ե�docker search tomcat.��������ֿⶼ��tomcat��ص�ʲô����

<img class="aligncenter" src="http://7xui79.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160630184927.png" width="689" height="413" />

һ��ѡ��star����߹ٷ��ľ���

[tomcat�ٷ�����](https://hub.docker.com/_/tomcat/)

docker pull tomcat

Ȼ��docker image �鿴���زֿ��ǲ��ǳ����ˡ�

һ��docker����tomcat���ŵ���8080�˿ڡ���run��ʱ����Ҫӳ������host���ض��˿ڣ����host��windows�����¾���default�������
<blockquote>Docker �ܹ������׵����úͰ�����˿ڡ������һ�������� ��ʶ(flags)�� 8080 ����д��������������ڲ��� 8080 �˿�ӳ�䵽���� Docker �����ĸ�λ�˿���(����˿ڵ�ͨ����Χ�� 32768 �� 61000)������Ҳ����ָ����ʶ����ָ���˿�8888��������</blockquote>
<span style="color: #ff0000;">docker run -it -p 8888:8080 -v /mnt/win10/:/opt/tomcat/webapp/ tomcat:8.0</span>

<span style="color: #ff0000;">�⽫��������ڲ��� 8080 �˿�ӳ�䵽���Ǳ��������� 8888 �˿��ϡ���������ڻ��ʣ�Ϊʲô����ֻʹ�� 1��1�˿�ӳ��ķ�ʽ���˿�ӳ�䵽 Docker ������ �����ǲ����Զ�ӳ���λ�˿ڵķ�ʽ������ 1:1 ӳ�䷽ʽ�ܹ���֤ӳ�䵽���������˿ڵ�Ψһ�ԡ���������Ҫ�������� Python Ӧ�ó������������ڲ������˶˿�8888��������û���㹻�� Docker �Ķ˿�ӳ�䣬��ֻ�ܷ�������һ����</span>

����docker������web���������ú��ˡ��ܼ򵥡���Ϊ�ٷ��ľ����ڲ�dockerfile�ļ��Ѿ��������jdk tomcat��д���ˡ��뿴����ļ�������github�鿴��

<a href="https://github.com/docker-library/tomcat/blob/8323df4824d3661f094a1a6c30ed7e13c0536b9e/8.0/jre8/Dockerfile">https://github.com/docker-library/tomcat/blob/8323df4824d3661f094a1a6c30ed7e13c0536b9e/8.0/jre8/Dockerfile</a>
<h1>����Ŀ¼</h1>
��Ϊ����һ������windows�����¿����ģ�����docker������linux�����²ſ������С�����windows�������ʹ�����������ˣ���Ҫ��windows�����Ŀ¼���ص����������������ڹ��ص�������Ŀ¼���棬����������tomcat/webapps/���档�����������war�ļ��Ϳ���ֱ����������ʹ�á�
<h3>����virtualbox��docker��������default�Ĺ���</h3>
��������ļ������ÿ����Ͻǵ���Ӱ�ť

<img class="aligncenter" src="http://f.hiphotos.baidu.com/exp/w=480/sign=107cd686ad51f3dec3b2b86ca4eff0ec/241f95cad1c8a786447d54426509c93d70cf5022.jpg" width="540" height="450" />

ѡ��֮ǰ�������õĹ����ļ��У���ʱһ�������Թ�ѡ�Զ�����

<img class="aligncenter" src="http://7xui79.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160630192055.png" width="628" height="381" />

���úù������󣬽���docker�����ϵͳ�����նˣ���ִ������ڹ��ص�Ŀ¼��ӡ�win10��Ŀ¼������ִ��"mount -t vboxsf warjar /mnt/win10/",������ɹ����ļ��е����á����סmount����һ��Ҫ���ϲ���-t vboxsf��warjar����windows10�¹����ļ������ƣ�/mnt/win10/����Ҫ��docker������й��صľ���·��
docker�����ϵͳĬ��ʹ��docker�û������ܻ�����Permission denied���󣬼�Ȩ�޲��㣬��Ҫ�л���root�˻�������ֻҪ���롰sudo su������ɣ���������
<h3>docker��������docker�������Ŀ¼</h3>
docker����֧�ְ�һ���������ϵ�Ŀ¼���ص������

docker run -it -p 8888:8080 -v /mnt/win10/:/opt/tomcat/webapp/ tomcat:8.0
ͨ��-v������ð��ǰΪ������Ŀ¼������Ϊ����·����ð�ź�Ϊ�����ڹ��ص�·����

���ھ����ھͿ��Թ�������������ļ��ˡ�
�����Ͱ�����windows��E:\warjarĿ¼�����ص���container��/opt/tomcat/webapp/Ŀ¼

����Ŀ¼���ɹ���д����Ŀ�������ֱ�ӽ�war�ŵ�E:\warjar��Ҳ���൱�ڷŵ���container��/opt/tomcat/webapp/��
<h1>���Ӧ����dockerִ��</h1>
��window��д��webӦ�û���spring bootӦ�á���һ�����Ϊwar��Ȼ��war�ŵ�E:\warjar��Ҳ���൱�ڷŵ���container��ʹ��default����������IP��ַ����ӳ���8080�˿����£�

docker run -it -p 8080:8080 -v /mnt/win10/:/opt/tomcat/webapp/ tomcat:8.0

<img class="aligncenter" src="http://7xui79.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160630184100.png" width="698" height="204" />

Ok.������ɡ��������Խ�ÿ��΢������Ϊjar����war������dockerʵ�ֽ���ʽ����ʵ��΢������

&nbsp;