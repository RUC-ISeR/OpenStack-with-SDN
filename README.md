# OpenStack-with-SDN
# HELLO WORLD AGAIN!
### 20170525/01:00
# 首先是horizon登录进去的时候一直提示invalid credentials。怀疑：
# 	1、keystone的原因。但是经过反复配置文件和验证操作都没有什么问题，遂百度；
# 	2、百度有一个给出来是role、user、project等关系可能配置错了。遂打算重新生成并指派一次。
# 于是开始删role，删完俩之后整个认证服务都死了，无法查看令牌，手动申请也没有用，更不要说重新创建role了。
# 尝试重新配置keystone，但是不论多少遍都是一样。尝试多次后解决。
# 1、停掉所有的neutron、nova服务，
# 2、把keystone彻底删除，包括配置文件 apt-get remove keystone --purge。这个完事儿之后还要把fernet-keys和ssl文件也给删掉。
# 3、reboot机器（不知道为撒要这么干）
# 4、重新apt-get install keystone，然后按照文档配置admin_token, connection, provider，完成文档的后续内容。
# 5、restart apache2 服务
# OK！

### 20170525/02:14
# 现在完成到装配完毕，依旧回到了最初的错误：horizon登录进去的时候一直提示invalid credentials
# 现在问题应该出在keystone中，输入keystone-all指令，得到ERROR信息主要是：

# 2017-05-25 01:58:08.042 12139 WARNING keystone.assignment.core [-] Deprecated: Use of the identity driver config to automatically configure the same assignment driver has been deprecated, in the "O" release, the assignment driver will need to be expicitly configured if different than the default (SQL).
# 2017-05-25 01:58:08.427 12139 WARNING root [-] Running keystone via eventlet is deprecated as of Kilo in favor of running in a WSGI server (e.g. mod_wsgi). Support for keystone under eventlet will be removed in the "M"-Release.
# 2017-05-25 01:58:08.429 12139 ERROR keystone.common.environment.eventlet_server [-] Could not bind to 0.0.0.0:35357
# 2017-05-25 01:58:08.430 12139 ERROR root [-] Failed to start the admin server
# 2017-05-25 01:58:08.430 12139 ERROR root error: [Errno 98] Address already in use

# 现在猜想是不是端口被占用了，但是我电脑没电了。。。

