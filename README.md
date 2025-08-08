# SLAM_con_ROS
Adaptación del código de https://articulatedrobotics.xyz/ para hacer SLAM con Lidar en nodos de ROS, se hizo en WLS con Ubuntu 22.04.5 LTS. Si necesita entender los nodos usa rqt_console. Pasos para continuar a partir de este? Navegación autonoma para exporar e ir creando el mapa o una vez con el mapa que el robot defina la major trayectoria para ir de A a B. 


## Comandos Proyecto ROS

### Comandos para hacer en cada nueva terminal
Puede configurarse un 'echo' para que se haga automaticamente cada vez que se abra la terminal, lo importante es configurar el underlay y overlay (los .bash), falta el comando de configurar la capa básica, además, la carpeta de trabajo donde se copia el repositorio se llama proyecto.
- cd proyecto/
- source install/setup.bash

A continuación,la mayoria de comandos para ponerlo a funcionar.

### Modifica - Agrega Nuevos Archivos
Cada vez que agreges un archivo a la carpeta de scr (o si es la primera vez) mete estos dos comandos, al hacer colcon creas tres carpetas más, si algunas vez colcon no avanza intenta hacer un paquete solamente o que colcon no haga todo en paralelo. Si es primera vez meta el comando para solucionar dependencias.
- colcon build --symlink-install
- source install/setup.bash


### Publicar Robot Básico
Una vez que no tengas errores en la terminal despues del comando source, puedes ingresar el siguiente comando; Este no habre ni Gazebo ni Rviz, solo genera los nodos del robot. Una vez usado se bloquea la terminal y no podras usarla hasta que termines el proceso con Control+C.  
- ros2 launch articubot_one rsp.launch.py

En otra terminal ingresa los comandos de los .bash y ejecuta el comando a continucación, este es unpaquete que se usa en los videos pero proviene de otro git, creará una ventana para mover las ruedas individualmente con un deslizador para ver como se mueven los ejes configura otra terminal y con el comando rviz2 habres el visualizador. 
- ros2 run joint_state_publisher_gui joint_state_publisher_gui

### Publicar Robot + Gazebo 
Con el siguiente comando generas el robot y se genera en gazebo (sin mapa).
- ros2 launch articubot_one launch_sim.launch.py

Puedes en otra terminal ejecutar el teleop para manejarlo con el teclado.
- ros2 run teleop_twist_keyboard teleop_twist_keyboard

### Publicar Robot + Mapa Gazebo
El primer comando genera el robot, Gazebo con el mapa. El segundo es el encargado de hacer SLAM, después de dejarlo cargar puedes susbribir Rviz a el topico de /map para que comience a crear el mapa.
- ros2 launch articubot_one launch_simu.launch.py
- ros2 launch slam_toolbox online_async_launch.py slam_params_file:=./scr/articubot_one/config/mapper_params_online_async.yaml use_sim_time:=true

