# SLAM_con_ROS
Adaptación de otro para hacer SLAM con Lidar en nodos de ROS


## Comandos

Comandos Proyecto ROS

cd proyecto/
source install/setup.bash


colcon build --symlink-install
source install/setup.bash


Publicar robot
ros2 launch articubot_one rsp.launch.py

Publicar robot conGazebo
ros2 launch articubot_one launch_sim.launch.py

Map
ros2 launch slam_toolbox online_async_launch.py slam_params_file:=./scr/articubot_one/config/mapper_params_online_async.yaml use_sim_time:=true


Manejo
ros2 run teleop_twist_keyboard teleop_twist_keyboard
ros2 run joint_state_publisher_gui joint_state_publisher_gui

rviz2
