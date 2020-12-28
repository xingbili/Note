### 执行shell脚本

```shell
#1. 方法一./shell脚本.sh
#2. 方法二：以绝对路径的方式去执行bash shell脚本
/data/shell/hello.sh
#3. 方法三：直接使用bash 或 sh 来执行bash shell脚本
① bash：
cd /data/shell
bash hello.sh
② sh：
cd /data/shell
sh hello.sh
#4.方法三：在当前的shell环境中执行bash shell脚本
cd /data/shell
. hello.sh
    或者
cd /data/shell
source hello.sh

```

