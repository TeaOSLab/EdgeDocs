# 手动安装边缘节点
1. 先在管理平台"创建节点"，填写节点的相关信息；
2. 可以在"集群节点" -- "安装升级" -- "手动安装" 界面中查看等待安装的边缘节点；
3. 在"手动安装"界面，可以查看配置文件内容，先不着急使用这个配置文件；
4. 在GoEdge官网上下载对应版本的边缘节点；
5. 上传到目标服务器，然后使用 `unzip` 命令解压，比如：
   ~~~bash
   unzip ./edge-node-linux-amd64-v0.0.1.zip
   ~~~
   如果系统没有 `unzip` 命令，请先安装；
6. 解压后转到安装目录下：
   ~~~bash
   cd edge-node/
   ~~~
   复制并修改配置文件：
   ~~~bash
   cp configs/api.template.yaml configs/api.yaml
   vi configs/api.yaml
   ~~~ 
   把 `api.yaml` 里面的内容换成在当前流程 第3步 看到的配置内容，然后保存；
7. 可以使用以下命令启动节点：
   ~~~bash
   bin/edge-node start
   ~~~
8. 可以使用 `ps` 命令确认进程是否正常启动：
   ~~~
   ps ax|grep edge-node
   ~~~
   应该输入类似于以下的内容：
   ~~~
   52160 ?        Sl     1:42 /opt/www/edge-node/bin/edge-node
   ~~~
9. 如果没有启动成功或者有其他异常，可以通过查看 `logs/run.log` 中的内容来诊断问题所在。   

## 确认启动状态
可以在单个集群的"集群节点"中查看节点的状态：
![集群节点列表](InstallManual1.png)   

正常情况下，状态应该为"运行中"。
   
## 注意事项
1. 单个服务器同时只能启动一个边缘节点。