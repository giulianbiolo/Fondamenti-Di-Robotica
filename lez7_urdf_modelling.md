<script type="text/javascript"
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [['$','$'], ['\\(','\\)']],
      processEscapes: true},
      jax: ["input/TeX","input/MathML","input/AsciiMath","output/CommonHTML"],
      extensions: ["tex2jax.js","mml2jax.js","asciimath2jax.js","MathMenu.js","MathZoom.js","AssistiveMML.js", "[Contrib]/a11y/accessibility-menu.js"],
      TeX: {
      extensions: ["AMSmath.js","AMSsymbols.js","noErrors.js","noUndefined.js"],
      equationNumbers: {
      autoNumber: "AMS"
      }
    }
  });
</script>

Fondamenti Di Robotica - Lezione 7  
==================================


----------------------------
## Modelling Robots and URDF  

Lo **Unified Robot Description Format** (URDF) è un formato XML per descrivere robot ed in particolare:  
- la struttura del robot (cinematica e superfici di collisione)  
- apparenza estetica  
- informazioni su velocità dei giunti e limiti di velocità  
- modelli di sensori tramite plugin (camera, LIDAR, etc.)  

Per migliorare la modularità e riutilizzabilità utilizziamo la macro language per XML chiamata **XACRO** che ci permette di scrivere file XML più leggibili con l'utilizzo dei parametri.  
XACRO permette di definire costanti, macro e semplici calcoli matematici, ciò semplifica molto i file URDF.  


----------
## LocoSim  

LocoSim è un framework dedicato alla simulazione di robot mobili e robot fissi. Dipende da ROS e da Pinocchio.  


-----------------
## Il Codice URDF  

Partiamo dal tag che descrive i **link** del robot:  
```xml
<link name="link_name">
    <inertial>...</inertial>
    <visual>...</visual>
    <collision>...</collision>
</link>
```
Il tag **visual** rappresenta l'aspetto del link, mentre il tag **collision** rappresenta la superficie di collisione.  
Il tag **inertial** contiene le informazioni su centro di massa e tensore d'inerzia del link.  
```xml
<inertial>
    <origin xyz="0 0 0" rpy="0 0 0"/>
    <mass value="1"/>
    <inertia ixx="1" ixy="0" ixz="0" iyy="1" iyz="0" izz="1"/>
</inertial>
```
Il tag **collision** fornisce una rappresentazione geometrica allo stesso modo del tag **visual** utilizzando un tag **geometry**.  
Si può settare uguale alla mesh visiva ma ciò comporterebbe un dispendio computazionale enorme, per cui spesso si utilizza una mesh più semplice come un parallelepipedo o se vogliamo essere precisi si può prendere la mesh visiva e farla passare per un programma come **MeshLab** per semplificare il modello riducendo molto il numero di vertici.  

Il tag **joint** descrive i giunti del robot:  
```xml
<joint name="joint_name" type="joint_type">
    <origin xyz="0 0 0" rpy="0 0 0"/>
    <parent link="parent_link"/>
    <child link="child_link"/>
    <axis xyz="0 0 0"/>
    <limit effort="0" velocity="0" lower="0" upper="0"/>
    <dynamics damping="0" friction="0"/>
</joint>
```
L'attributo **type** descrive il tipo di giunto, che sia revolute, prismatic, fixed, etc... Inoltre contiene un parent e un child che sono i link che il giunto collega.  
Il tag **axis** descrive l'asse di rotazione del giunto.  
Il tag **limit** descrive i limiti di rotazione del giunto.  

L'elemento **transmission** è un'estensione al formato URDF che permette di descrivere un rapporto tra il giunto ed il suo attuatore.  
```xml
<transmission name="shoulder_lift_trans">
    <type>transmission_interface/SimpleTransmission</type>
    <joint name="shoulder_lift_joint">
        <hardwareInterface>hardware_interface/EffortJointInterface</hardwareInterface>
    </joint>
    <actuator name="shoulder_lift_motor">
        <hardwareInterface>hardware_interface/EffortJointInterface</hardwareInterface>
        <mechanicalReduction>1</mechanicalReduction>
    </actuator>
</transmission>
```
Il tag **type** descrive il tipo di trasmissione, il tag **joint** descrive il giunto, il tag **actuator** descrive l'attuatore.
Generalmente si utilizza questo tag **transmission** quando il giunto è collegato ad un attuatore tramite un riduttore, o comunque il movimento dell'attuatore non è lo stesso diretto movimento nel giunto.  


----------------------
## Visualizing in RViz  

LocoSim fornisce una funzione dedicata per pubblicare lo stato dei giunti durante runtime e renderli disponibili per RViz.  
Un modo conveniente di setuppare l'environment di nodi utilizzati è tramite un file launch.  
```xml
<?xml version="1.0"?>
<launch>
    <include file="$(find loco_sim)/launch/upload.launch"/>
    <node pkg="joint_state_publisher_gui" type="joint_state_publisher_gui" name="joint_state_publisher_gui" />
    <node pkg="robot_state_publisher" type="robot_state_publisher" name="robot_state_publisher" />
    <node pkg="rviz" type="rviz" name="rviz" args="-d $(find loco_sim)/rviz/conf.rviz" />
</launch>
```

[ Pagina 24 / 52 ]  
