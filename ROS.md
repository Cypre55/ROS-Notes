# ROS

#### catkin_make

```bash
source <dir_where_catkin_make_is_used>/devel/setup.bash
```

```bash
# Gives the locations it pulls the packages from
echo $ROS_PACKAGE_PATH
```

```bash
# to build a package
# in a catkin workspace
catkin_make
catkin_make install # (optionally)
```

#### Filesystem

- **Packages** - Packages are the software organization unit of ROS code. Each package can contain libraries, executables, scripts, or other artifacts.
- **Manifests**(package.xml) -  A manifest is a description of a *package*. It serves to define dependencies between *packages* and to capture meta information about the *package* like version, maintainer, license, etc...
- The `build` folder is the default location of the build space and is where `cmake` and `make` are called to configure and build your packages. The `devel` folder is the default location of the devel space, which is where your executables and libraries go before you install your packages.

##### rospack

```bash
# Gives the directory in which the package is present
rospack find [package_name]
```

```bash
# to get first-order dependencies
rospack depends1 [package_name]
```

```bash
# to get indirect dependencies
rospack depends [package_name]
```



##### roscd

```bash
# cd's into the package directory
roscd [locationname[/subdir]]
```

```bash
# this takes you to the folder the log files are stored
roscd log
```

##### rosls

```bash
# performs ls in a package by name
rosls [locationname[/subdir]]
```

#### catkin Packages

- The package must contain a catkin compliant package.xml file.
  - That package.xml file provides meta information about the package.
- The package must contain a CMakeLists.txt which uses catkin.
  - If it is a catkin meta-package it must have the relevant boilerplate CMakeLists.txt file.
- Each package must have its own folder
  - This means no nested packages nor multiple packages sharing the same directory.

To create a catkin package,  enter the src directory in your catkin workspace.

```bash
catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
```

Within the package.xml file, <build_depend> tags are created automatically when the above command is run. These are the dependencies that are available at buildtime.

```xml
<build_depend>[package_name]</build_depend>
```

To have them present at runtime, we can add <exec_depend> tag.

```xml
<exec_depend>[package_name]</exec_depend>
```

#### ROS Graph Concepts

- Nodes: A node is an executable that uses ROS to communicate with other nodes.
- Messages: ROS data type used when subscribing or publishing to a topic.
- Topics: Nodes can *publish* messages to a topic as well as *subscribe* to a topic to receive messages.
- Master: Name service for ROS (i.e. helps nodes find each other)
- rosout: ROS equivalent of stdout/stderr
- roscore: Master + rosout + parameter server

#### roscore

Like mentioned above, roscore is  Master + rosout + parameter server.

```bash 
roscore
```

#### rosnode

```bash
# List of running ROS Nodes
rosnode list
```

```bash
# Information about a specific node
rosnode info <node_name>
```

```bash
# Check if node is up
rosnode ping <node_name>
```



#### rosrun

```bash
rosrun [package_name] [node_name]
```

