---
title: Ubuntu配置FTP服务器
date: 2021-10-14 10:06:20
toc: true
tags:
    - Linux
---

用 `vsftpd -v` 查看是否安装了 vsftpd，如果没有，安装它

{% codeblock lang:bash line_number:false %}
sudo apt-get install vsftpd
{% endcodeblock %}

<!--more-->

编辑 `/etc/vsftpd.conf` 配置文件

{% codeblock /etc/vsftpd.conf line_number:true %}
listen=NO
listen_ipv6=YES
anonymous_enable=NO
write_enable=YES
dirmessage_enable=YES
use_localtime=YES
xferlog_enable=YES
connect_from_port_20=YES
secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
ssl_enable=NO
{% endcodeblock %}

启动vsftpd应用新的更改

{% codeblock lang:bash line_number:false %}
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
sudo service vsftpd start
{% endcodeblock %}

如果要用macOS访达的 ⌘K 连接服务器，需要关闭VPN。

<br/>
