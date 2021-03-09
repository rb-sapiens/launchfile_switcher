# launchfile_switcher
ROS package for management launch files. 
This package provides features that easily switch launch files.

## Building
Build as standard catkin packages. There are no special dependencies needed. 

# ROS API
## launchfile_switcher
### Subscribed Topics

- /mode (std_msgs/String)
This topic indicates the next mode name. Modes can be defined in a yaml file (an example is below).


### config file example
- mode_list.yaml

```
mode_list:
    normal:
        launch:
            - pkg: your_robot_package
              file: /launch/your_robot_start.launch
              args:
                - name: mode
                  value: single_camera
                - name: is_device
                  value: false
            - pkg: your_navigation_package
              file: /launch/your_navigation_start.launch
              args:
                - name: mode
                  value: single_camera
                - name: explore
                  value: false
    make_map:
        launch:
            - pkg: your_robot_package
              file: /launch/your_robot_start.launch
              args:
                - name: mode
                  value: single_camera
                - name: is_device
                  value: false
            - pkg: your_navigation_package
              file: /launch/your_navigation_start.launch
              args:
                - name: mode
                  value: single_camera
                - name: explore
                  value: true
```

The example yaml config file above has two modes which equal to: 

normal
```
  <include file="$(find your_robot_package)/launch/your_robot_start.launch">
    <arg name="mode" value="single_camera"/>
    <arg name="is_device" value="false"/>
  </include>
  <include file="$(find your_navigation_package)/launch/your_navigation_start.launch">
    <arg name="mode" value="single_camera"/>
    <arg name="explore" value="false"/>
  </include>
```

make_map
```
  <include file="$(find your_robot_package)/launch/your_robot_start.launch">
    <arg name="mode" value="single_camera"/>
    <arg name="is_device" value="false"/>
  </include>
  <include file="$(find your_navigation_package)/launch/your_navigation_start.launch">
    <arg name="mode" value="single_camera"/>
    <arg name="explore" value="true"/>
  </include>
```

### launch file sample
```
  <node pkg="launchfile_switcher" type="launchfile_switcher" name="launchfile_switcher" output="screen">
    <param file="$(find your_package)/config/mode_list.yaml" command="load" />
  </node>
```