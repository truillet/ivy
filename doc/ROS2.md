# compiler un noeud ROS

Après avoir installer ROS2 (Foxy), installer colcon (**col**lective **con**struction

``sudo apt install python3-colcon-common-extensions``

Créer un nouveau worspace (le nom importe peu, par exemple *ros2*). Y créer un nouveau répertoire *src*. Tous vos packages se situeront dans ce reptoire *~/ros2/src*

Pour compiler votre package, se postionner dans *~/ros2/src* et taper les commandes :

``colcon build --packages-select <votre package>

. install.setup.bash

ros2 run <votre package> <votre noeud>``

Si vosus souhaitez voir la liste des topics actifs :

``ros2 topic list -t``
