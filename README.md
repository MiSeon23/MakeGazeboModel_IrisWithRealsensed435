# Gazebo_Modeling

### with px4


* * *


## **How to put the intel_realsense_d435_camera to iris(quadrotor)**


### 1. Download files about sensor
  It have to contain ~.dae, ~.urdf.xacro, ~.config, ~.sdf files.
   
   
### 2. Make new sensor directory in your model directory
  ```
  $ cd ~/Firmware/Tools/sitl_gazebo/models    
  $ mkdir realsense_d435
  ```
  
  
### 3. Move downloaded files into the models/new_made_sensor_directory and models/rotors_description directory
  ```
  $ mv ~/realsense_d435_Gazebo/model.config ~/Firmware/Tools/sitl_gazebo/models/realsense_d435
  $ mv ~/realsense_d435_Gazebo/model.sdf ~/Firmware/Tools/sitl_gazebo/models/realsense_d435
  $ mv ~/realsense_d435_Gazebo/meshes/d435.dae ~/Firmware/Tools/sitl_gazebo/models/rotors_description/meshes
  $ mv ~/realsense_d435_Gazebo/urdf/materials.urdf.xacro ~/Firmware/Tools/sitl_gazebo/models/rotors_description/meshes     
  $ mv ~/realsense_d435_Gazebo/urdf/d435.urdf.xacro ~/Firmware/Tools/sitl_gazebo/models/rotors_description/urdf
  ```


### 4. Edit iris.xacro
  ```
  $ cd ~/Firmware/Tools/sitl_gazebo/models/rotors_description/urdf
  $ gedit iris.xacro
  ```
  
   Open file d435.urdf.xacro
  
   Copy all below <!-- includes --> without </robot> at the end of it
  
   Paste it on the </robot> at the end of the iris.xacro
  
   Then, edit filenames
   
    first filename -> "metarials.urdf.xacro"
    second filename -> "model://rotors_description/meshes/d435.dae"
   
   
### 5. Edit iris.sdf
  ```
  $ cd ~/Firmware/Tools/sitl_gazebo/models/iris
  $ gedit iris.sdf
  ```
  
  Add the follwing on the </model> at the end of the iris.sdf
  
  ```
    <include>
      <uri>model://realsense_d435</uri>    
      <pose>0 0 0.15 0 0 3.14159265</pose>
    </include>
    <joint name"realsense_d435_joint" type"fixed">
      <child>realsense_camera::link</child>    
      <parent>base_link</parent>
    </joint>
  ```
  
  
### 6. EXECUTE!
  ```
  $ cd ~/Firmware
  $ make posix_sitl_default gazebo
  ```
