# Create a ROS Workspace
## + create a catkin workspace: 
```
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/src
$ catkin_init_workspace
```
```
$ cd ~/catkin_ws/
$ catkin_make
```
To make sure your workspace is properly overlayed by the setup script, make sure ROS_PACKAGE_PATH environment variable includes the directory you're in. 
```
$ echo $ROS_PACKAGE_PATH
/home/albert/catkin_ws/src:/opt/ros/kinetic/share
```

## + Creating a ROS Package
Packages in a catkin Workspace       
***catkin_create_pkg*** 命令 requires that you give it a package_name and optionally a list of dependencies on which that package depends:     
```
# This is an example, do not try to run this
# catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
```
eg: create a new package called 'beginner_tutorials' which depends on std_msgs, roscpp, and rospy:
```
$ catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
```

----
## **步骤：**
1. Create a ROS Workspace:
```
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/src
$ catkin_init_workspace

$ cd ~/catkin_ws/
$ catkin_make

$ source devel/setup.bash

$ echo $ROS_PACKAGE_PATH
```
2. Creating a ROS Package
```
$ catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
```
3. Building a catkin workspace and sourcing the setup file
```
$ cd ~/catkin_ws
$ catkin_make
#To add the workspace to your ROS environment you need to source the generated setup file: 
$ . ~/catkin_ws/devel/setup.bash
```

----

### 查看一个package 的依赖包: 
```
#查看直接引用 的
$ rospack depends1 beginner_tutorials 

#查看包括直接和间接的所有引用：
$ rospack depends beginner_tutorials
```


## + ROS Filesystem
**Packages:** Packages are the software organization unit of ROS code. Each package can contain libraries, executables, scripts, or other artifacts.

**Manifests (package.xml):** A manifest is a description of a package. It serves to define dependencies between packages and to capture meta information about the package like version, maintainer, license, etc...

**Commands**:

- ***rospack*** allows you to get information about packages. In this tutorial, we are only going to cover the find option, which returns the path to package.  
    eg:
     ```
    rospack find [package_name]
    $ rospack find roscpp
    ```
- ***roscd*** is part of the rosbash suite. It allows you to change directory (cd) directly to a package or a stack.        
    ```
    $ roscd [locationname[/subdir]]
    $ roscd roscpp
    ```
- ***roscd log*** will take you to the folder where ROS stores log files. Note that if you have not run any ROS programs yet, this will yield an error saying that it does not yet exist.
    ```
    $ roscd log
    ```      
- ***rosls*** is part of the rosbash suite. It allows you to ls directly in a package by name rather than by absolute path.     
    ```
    $ rosls [locationname[/subdir]]
    $ rosls roscpp_tutorials
    ```



