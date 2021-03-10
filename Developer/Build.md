# 源码编译
要想从源码运行或者编译GoEdge，需要分别编译EdgeAdmin、EdgeAPI、EdgeNode等组件。

当前文档中的"下载"可以使用zip下载的方式，也可以使用`git clone`，建议使用后者更容易维护。

## 整体源码结构
从Github对应仓库下载各个组件的源码后，建议的整体源码结构为：
~~~
EdgeProject/
   EdgeAdmin     # 管理平台
   EdgeAPI       # API节点
   EdgeNode      # 边缘节点
   EdgeCommon    # 公共依赖
   ....
~~~

## 运行环境
* 操作系统：目前只支持Mac OS和Linux开发环境；
* MySQL：支持 v5.7.x 以上；
* Golang：支持 v1.14以上。

## 公共依赖源码
`EdgeCommon`是各个组件公共依赖的源码，下载地址 [https://github.com/TeaOSLab/EdgeCommon](https://github.com/TeaOSLab/EdgeCommon) 。

## 编译各个组件

### 编译EdgeAdmin管理平台
1. 从 [https://github.com/TeaOSLab/EdgeAdmin](https://github.com/TeaOSLab/EdgeAdmin)下载EdgeAdmin源码；
2. 从 [https://github.com/TeaOSLab/EdgeCommon](https://github.com/TeaOSLab/EdgeCommon)下载EdgeCommon源码，如果已经下载则不需要重复下载；
3. 将EdgeAdmin和EdgeCommon放在同一目录下；
4. 转到 `EdgeAdmin` 目录下；
5. 执行 `go mod tidy` 下载项目依赖的源码；   
6. 复制 `build/configs/server.template.yaml` 到 `build/configs/server.yaml`，如果 `server.yaml` 已经存在则无需重复复制；这个文件里默认指定了管理平台的访问端口为`7788`，可以根据自己的需要进行修改；
7. 复制 `build/configs/api.template.yaml` 到 `build/configs/api.yaml`；这个文件默认指定了API节点的端口为`8003`，在启动API节点时如果修改了端口号，也要在这里进行同步的修改；   
8. 运行 `go run cmd/edge-admin/main.go`

如果想编译整个项目，请参考 `build/build.sh`，比如可以运行：
~~~bash
./build.sh linux amd64
~~~
来编译`linux/amd64`版本的项目压缩包，编译后生成的压缩包可以在`dist`目录下找到。

### 编译EdgeAPI API节点
API节点是唯一可以操作数据库的节点，所以需要在步骤中配置数据库，也是其他节点依赖运行的节点。

1. 从 [https://github.com/TeaOSLab/EdgeAPI](https://github.com/TeaOSLab/EdgeAPI)下载EdgeAPI源码；
2. 从 [https://github.com/TeaOSLab/EdgeCommon](https://github.com/TeaOSLab/EdgeCommon)下载EdgeCommon源码，如果已经下载则不需要重复下载；
3. 将EdgeAdmin和EdgeCommon放在同一目录下；
4. 转到 `EdgeAPI` 目录下；   
5. 执行 `go mod tidy` 下载项目依赖的源码；
6. 复制 `build/configs/api.template.yaml` 到 `build/configs/api.yaml`，如果 `api.yaml` 已经存在则无需重复复制；然后修改其中的配置 `nodeId` 为API节点的ID，`secret` 为API节点的密钥；如果还没有创建过API节点，则可以在修改数据库配置（第7步）后，通过执行 `go run cmd/edge-api/main.go setup -api-node-protocol=http -api-node-host=127.0.0.1 -api-node-port=8003` 初始化数据库，然后在执行后的控制台提示或者数据库 `edgeAPINodes`中获取节点ID（字段`uniqueId`）和密钥（字段`secret`）；
7. 复制 `build/configs/db.template.yaml` 到 `build/configs/db.yaml`，并修改其中的数据库配置；
8. 运行 `go run cmd/edge-api/main.go`。

如果想编译整个项目，请参考 `build/build.sh`，比如可以运行：
~~~bash
./build.sh linux amd64
~~~
来编译`linux/amd64`版本的项目压缩包，编译后生成的压缩包可以在`dist`目录下找到。

### 编译EdgeNode边缘节点
1. 从 [https://github.com/TeaOSLab/EdgeNode](https://github.com/TeaOSLab/EdgeNode)下载EdgeNode源码；
2. 从 [https://github.com/TeaOSLab/EdgeCommon](https://github.com/TeaOSLab/EdgeCommon)下载EdgeCommon源码，如果已经下载则不需要重复下载；
3. 将EdgeNode和EdgeCommon放在同一目录下；
4. 转到 `EdgeNode` 目录下；
5. 执行 `go mod tidy` 下载项目依赖的源码；   
6. 复制 `build/configs/api.template.yaml` 到 `build/configs/api.yaml`，如果 `api.yaml` 已经存在则无需重复复制；然后修改其中的配置；如果你还没有边缘节点，需要先运行EdgeAdmin并通过界面创建一个节点后再修改配置后运行边缘节点；
7. 运行 `go run cmd/edge-node/main.go`。

如果想编译整个项目，请参考 `build/build.sh`，比如可以运行：
~~~bash
./build.sh linux amd64
~~~
来编译`linux/amd64`版本的项目压缩包，编译后生成的压缩包可以在`dist`目录下找到。
