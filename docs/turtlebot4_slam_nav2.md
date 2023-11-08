# Turtlebot4 Slam and Navigation (ubuntu 22.04, ros2, humble)

#### Humble installation
https://docs.ros.org/en/humble/Installation.html

#### Turtlebot4 installation

    $ sudo apt update && sudo apt install ros-humble-turtlebot4-desktop

#### Turtlebot4 setup
https://turtlebot.github.io/turtlebot4-user-manual/setup/basic.html

Password to ssh in rpi is turtlebot4
##
### Update create3 firmware

goto irobot webpage ==> update ==> select humble ==> update
##

###  Properly source the bashrc
![Alt text](image.png)
##

### Enter or delete namespace from the robot

 ssh in rpi (password- turtlebot4)

     $ turtlebot4-setup

ros setup ==> bash setup ==> ROBOT_NAMESPACE[]

### Install fast dds
    $ sudo apt update

    $ sudo apt install fastddsgen

### Edit ntp.config
got irobot==> Beta features ==> edit ntp.config 

paste following lines in the box as it is.

        # Use RPi4 as preferred server
        # Minpoll 2^4 = 16s
        # Maxpoll 2^6 = 64s
        server 192.168.186.3 prefer iburst minpoll 4 maxpoll 6

save
### Slam

https://turtlebot.github.io/turtlebot4-user-manual/tutorials/generate_map.html

### navigation

https://turtlebot.github.io/turtlebot4-user-manual/tutorials/navigation.html

Commands should be used including the robot namespace if the robot has its own namespace

for eg.:

        $ ros2 launch turtlebot4_navigation slam.launch.py namespace:=/robot1

        $ ros2 launch turtlebot4_navigation localization.launch.py map:=office.yaml namespace:=/robot1

        $ ros2 launch turtlebot4_navigation nav2.launch.py namespace:=/robot1
##
### tf tree

* If ROBOT HAS THE NAMESPACE then the topics published will also have the namespace.
* In this case, tf tree will NOT be visible using $ ros2 run rqt_tf_tree rqt_tf_tree

for that reson use tf_relay (not required if robot does not have a namespace)

github:

https://github.com/swarmBots-ipa/tf_relay

download the packages in the workspace.

after running localisation, nav2, rviz open a new tab, goto workspace, source it and run:


    $ ros2 run tf_relay relay

in a new tab after ruuning the following command tf tree will be visible.

    $ ros2 run rqt_tf_tree rqt_tf_tree

note: a certain processing time needs to be given to load the tf tree.
##

### Turtlebot fails to avoid obstacles (fix)
githug issue link:

https://github.com/turtlebot/turtlebot4/issues/247

go to computer/opt/ros/humble/share/turtlebot_navigation/config and open a terminal.

run the commands to make suggested changes in nav2.yaml and localisation.yaml file in the github issues.

    $ sudo gedit nav2.yaml

    $ sudo gedit localization.yaml








  










