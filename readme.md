
##Distributed Task Queue 分布式任务队列框架

  `Distributed Task Queue` 是一个简单的分布式框架,核心原理是**由任务服务器分配代码到各个任务执行的主机**,换句话说也就是**远程代码执行**,只需要在跑任务的机器上布置任务执行模块,无需做更多的操作即可实现分布式任务执行
  
##How to using Distributed Task Queue 

  `task_server` 是任务派遣服务器,最后封装好`task_add_task_handle` 再来补充这里<br/><br/>

  `task_client` 是执行任务的模块,只需要运行这个Python 即可,`task_client.py` 依赖`requests` ,在布置的时候记得需要安装它

##Distributed Task Queue 的其他细节

####远程代码执行与任务执行

  执行任务的主机尽量简单布置,最好能让一个模块就能够做很多的事情,所以把代码当作是一个任务来执行是不错的解决方案,首先可以解决掉复杂的任务语句处理(就像Windows 的控制台解析批处理文件一样,会使得执行任务的模块变得臃肿而且拓展性不高),除去Python 可以执行分配下来的任务,几乎支持所有可以使用`eval()` 执行的语言(无论是Python 还是JavaScript 等),不受执行的平台所限制(即便是作为本地进程来运行的Python ,还是浏览器的前端JavaScript 都可以领取任务执行)<br/>

  派遣到主机分为两种任务:`single_task` (单任务)和`multiple_task` (多任务),`multiple_task` 相当于提供一组`single_task` 单任务列表,让执行任务的主机按照顺序来执行每个任务

---

####关于任务的负载均衡

  关于任务的负载均衡使用简单的遍历算法,让任务数较多的主机把自己的任务分配到任务比较少的主机,尽可能让每个执行任务的主机都能够平衡执行任务的压力,关于分配的算法写在`task_dispatch.dispatch()` 中

---

####任务服务器的维护备份

  这部分还在开发,下次补上

