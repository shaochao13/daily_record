# Create a ROS Workspace
## 1. create a catkin workspace: 
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

## 2. ROS Filesystem
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



