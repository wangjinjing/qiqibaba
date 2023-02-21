# ros

## 安装ROS
官方安装文档参见[链接](http://wiki.ros.org/kinetic/Installation/Ubuntu)
ubuntu 16.04当前使用的ROS版本为kinetic
ubuntu 18.04当前使用的ROS版本为melodic
ubuntu 20.04当前使用的ROS版本为noetic

1. 安装ros的安装源
    ```bash
    sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ $DISTRIB_CODENAME main" > /etc/apt/sources.list.d/ros-latest.list'
    #sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.ustc.edu.cn/ros/ubuntu/ $DISTRIB_CODENAME main" > /etc/apt/sources.list.d/ros-latest.list'
    ```
2. 安装ROS public GPG key
    ```bash
    sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
    # 如果上面的命令执行失败，可以用下面的命令代替
    #curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
    ```
3. 更新apt仓库cache
    ```bash
    sudo apt-get update
    ```
4. 安装ROS完整版
    ```bash
    # ubuntu 16.04
    sudo apt-get install ros-kinetic-desktop-full
    # ubuntu 18.04
    #sudo apt-get install ros-melodic-desktop-full
    # ubuntu 20.04
    #sudo apt-get install ros-noetic-desktop-full
    ```
5. 初始化rosdep
    ```bash
    sudo c_rehash /etc/ssl/certs
    sudo rosdep init
    rosdep update
    ```
6. 配置环境变量 

    Ubuntu使用bash作为默认的shell，执行以下命令即可
    ```bash
    echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
    #echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
    #echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    ```
    ROS还支持zsh，如果使用zsh作为默认shell，可以执行以下命令
    ```bash
    echo "source /opt/ros/kinetic/setup.zsh" >> ~/.zshrc
    #echo "source /opt/ros/melodic/setup.zsh" >> ~/.zshrc
    #echo "source /opt/ros/noetic/setup.zsh" >> ~/.zshrc
    source ~/.zshrc
    ```


## 如何导出interface目录下的消息供rospy使用

编译完成后，在output目录下会生成ros消息相关的包，通过执行下面的命令，就可以在python代码中访问interface目录下定义的消息结构

```bash
source  output/setup.bash
```

如果使用的默认shell是zsh，可以用下面的命令替代

```zsh
source  output/setup.zsh
```

也可以在python代码中使用下面的代码

```python
import sys
sys.path.append("../output/ros/lib/python2.7/dist-package")
```

然后在python代码中导入相关的消息包，就可以了直接使用了

```python
from  grabber_msgs.msg  import DaoYuanIns
ins = DaoYuanIns()
print ins
```

