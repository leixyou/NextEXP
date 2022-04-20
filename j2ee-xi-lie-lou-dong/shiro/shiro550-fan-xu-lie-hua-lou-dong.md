# shiro550反序列化漏洞

Apache Shiro是一个开源安全框架，它提供了身份验证、授权、加密和会话管理。Shiro的框架直观且易于使用，同时提供了强大的安全性。在Apache Shiro 1.2.4及更早的版本中，加密的用户信息被序列化并存储在一个名为remember-me的Cookie中。攻击者可以使用Shiro的默认密钥伪造用户cookie，触发Java反序列化漏洞，然后在目标机器上执行任意命令。

<=1.2.4硬编码密钥为：kPH+bIxk5D2deZiIxcaaaA==

在1.2.4之后的版本，一旦攻击者在知道了密钥后，就可以构造恶意payload，经过序列化、AES加密、base64编码操作加工后，作为cookie的rememberMe字段发送。Shiro将rememberMe进行解密并且反序列化，最终造成反序列化漏洞，进而在目标机器上执行任意命令。部分工具会内置一批密钥，一旦命中已知的密钥，即使是如1.4.2版本的，也可以RCE。如下图：

![](../../.gitbook/assets/shiro\_rce.png)



