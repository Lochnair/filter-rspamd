我是光年实验室高级招聘经理。
我在github上访问了你的开源项目，你的代码超赞。你最近有没有在看工作机会，我们在招软件开发工程师，拉钩和BOSS等招聘网站也发布了相关岗位，有公司和职位的详细信息。
我们公司在杭州，业务主要做流量增长，是很多大型互联网公司的流量顾问。公司弹性工作制，福利齐全，发展潜力大，良好的办公环境和学习氛围。
公司官网是http://www.gnlab.com,公司地址是杭州市西湖区古墩路紫金广场B座，若你感兴趣，欢迎与我联系，
电话是0571-88839161，手机号：18668131388，微信号：echo 'bGhsaGxoMTEyNAo='|base64 -D ,静待佳音。如有打扰，还请见谅，祝生活愉快工作顺利。

# filter-rspamd

## Description
This filter implements the Rspamd protocol and allows OpenSMTPD to request an Rspamd analysis
of an SMTP transaction before a message is committed to queue.


## Features
The filter currently supports:

- greylisting
- adding X-Spam related headers to a message
- rewriting Subject
- DKIM-signing message
- Rspamd-provided SMTP replies
- Allow Rspamd to add and remove headers


## Dependencies
The filter is written in Golang and doesn't have any dependencies beyond standard library.

It requires OpenSMTPD 6.6.0 or higher.


## How to install
Install from your operating system's preferred package manager if available.
On OpenBSD:
```
$ doas pkg_add opensmtpd-filter-rspamd
quirks-3.167 signed on 2019-08-11T14:18:58Z
opensmtpd-filter-rspamd-0.1.x: ok
$
```

Alternatively, clone the repository, build and install the filter:
```
$ cd filter-rspamd/
$ go build
$ doas install -m 0555 filter-rspamd /usr/local/libexec/smtpd/filter-rspamd
```


## How to configure
The filter itself requires no configuration.

It must be declared in smtpd.conf and attached to a listener for sessions to go through rspamd:
```
filter "rspamd" proc-exec "filter-rspamd"

listen on all filter "rspamd"
```

A remote rspamd instance can be specified by providing the -url parameter to the filter:
```
filter "rspamd" proc-exec "filter-rspamd -url http://example.org:11333"

listen on all filter "rspamd"
```


Any configuration with regard to thresholds or enabled modules must be done in rspamd itself.
