![关注二维码](https://img-blog.csdnimg.cn/20190117103222240.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZpdmUz,size_16,color_FFFFFF,t_70)

# 说明
HProxy是一个基于HOST的HTTP代理，它与普通代理的不同之处如下：

| 对比项 | 普通代理 | HOST代理 |
| --- | --- | --- |
| 需要客户端支持 | 是 | 否 |
| 设置方式 | 配置客户端 | 配置HOST |
| 支持透明代理 | 是 | 是 |
| 支持绝对路径 | 是 | 否 |
| 支持非80端口 | 是 | 否 |
| 实现方式 | socket | http |
| URL路径支持 | 绝对路径 | 相对路径 |
| 代理服务与客户端同机 | 支持 | 不支持 |
| 代理配置方式 | 域名配置灵活 | host配置不灵活 | 

# 安装
```bash
pip install git+https://github.com/five3/hproxy.git
```

# 使用
使用这个库也很简单，它只接收一个参数，用于指定插件脚本的路径，可以是绝对路径和相对路径。插件文件样例如下：
```python
from plugins import before_proxy, after_proxy

@before_proxy
def before(context):
    print(context)

@after_proxy
def after(context):
    print(context)

```
插件脚本写完后，执行如下命令即可启动`http`代理服务。
```bash
hproxy -s /path/to/script.py
```
接着，在需要使用代理的机器上添加对应的host，假设代理服务所在ip为10.0.0.1，需要代理www.testqa.cn域名。则添加如下：
```bash
10.0.0.1 www.testqa.cn
```
> 注意：代理服务和需要使用代理的机器不能是同一个ip，否则就死循环了。

最后，通过浏览器或者程序来访问www.testqa.cn域名，则会看到插件脚本中打印的信息。

# 应用
- mock
- api测试

# 后期计划
- 协程支持
- 过滤功能
- https支持
- websocket支持
- keep-alive支持
- chunk支持