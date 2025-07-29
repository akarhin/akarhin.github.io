---
layout: page
title: D-bot
description: Implementation of machine-to-machine communication through an AGV.
img: assets/img/m2m.jpg
importance: 3
category: fun
giscus_comments: true
---

This project explores the implementation of Machine-to-Machine (M2M) communication in industrial settings, focusing on the integration of Automated Guided Vehicles (AGVs) with non-integrated industrial equipment such as cranes. By employing a three-wheel differential drive mobile robot equipped with 3D-lidar and ultra-wideband radio signal systems for navigation and localization, the AGV demonstrates effective M2M communication capabilities. The results highlight the potential of AGVs to autonomously collaborate with various industrial machines, enhancing automation and operational efficiency.

## Introduction:

Industrial environments often face challenges in coordinating multiple machines due to limited space and scheduling constraints, leading to downtime and inefficiencies. M2M communication technology aims to facilitate autonomous interaction among smart devices, improving cost efficiency and time management without extensive integration efforts. AGVs, as mobile robots, offer a solution by autonomously transporting goods and utilizing sensor data and object detection algorithms for efficient navigation and task execution. This along with further trends in Industrial internet of things (IIoT) have lead to a large quantity of continuous industrial data being gathered from factory floors. This data is used to monitor and control industrial processes to become more efficient, reduce errors, prevent theft, and incorporate complex organizational systems. In order to operate automatically, AGVs already communicate with other equipment, perhaps through a digital twin or wireless networks for proper integration to the factory floor. Utilizing an AGV as a communication hub for industrial machinery provides a promising premise.

This project introduces a case study of an AGV capable of M2M communication between itself and non-integrated industrial machines, specifically a crane and an ultra-wideband radio signal system. The study demonstrated the effectiveness of the AGVs M2M communication while providing a starting point for further research and development in the field of M2M communication with the AGV. This study was part of the Proceedings of the 8th Baltic Mechatronics Symposium [https://aaltodoc.aalto.fi/items/ebbb5b20-1f83-46b0-91bd-9e92ed2685d7].


## Methods:

The case study involved a three-wheel differential drive AGV communicating with an overhead crane and an ultra-wideband radio signal system. The AGV used a 3D-lidar for navigation, and real-time measurements were integrated with a pre-measured point cloud map for accurate localization. Communication was established via HTTP requests and WebSocket protocols, enabling the AGV to interact with the crane for precise load positioning and maintaining a safety zone within the crane's operating area. The AGV communicated with the crane to estimate the hook position so that it could navigate to a position where a load could be received from the crane. Inside the crane operating area, a safety zone was established by applying the ultra-wideband radio signal system. That is, if a worker wearing a tag entered the area, all crane and AGV function would seize until the tag left the area. Safety zone reaction speed was tested with two tag placements: hung around the workers neck and attached to the waist of the worker. During operation of the test task, the AGV generated a log file to document its operations. This log file included details such as timestamp, location, and task status, and was updated every 0.5 seconds. 

{% include figure.liquid path="assets/img/m2m_handsome.jpg" %}

{% include figure.liquid path="assets/img/m2m_agv_annotated.png" %}

{% include figure.liquid path="assets/img/ROS_architecture.png" %}

{% include figure.liquid path="assets/img/ilmatar.jpg" %}


## Results:

The AGV successfully demonstrated M2M communication by accurately receiving the crane's hook position and initiating a safety zone. The reaction speed of the safety zone varied based on the placement of personnel tags, with mean reaction times of 12.92 seconds (waist) and 19.38 seconds (neck). The localization accuracy was within acceptable industrial ranges, validating the AGV's navigation capabilities with. Notably, there was a significant difference of safety zone reaction speed between the two placements of the personnel tag. 




{% include figure.liquid path="assets/img/floorplan.jpg" %}

{% include figure.liquid path="assets/img/m2m_table.png" %}

## Discussion:

The purpose of this study was to construct an AGV with an ultra-wideband radio signal system and demonstrate its ability to perform M2M communication with industrial equipment. The results indicated successful implementation of the AGV, providing a promising solution for automating tasks involving non-integrated industrial equipment. The presented implementation serves as a starting point for further research and development of M2M communication and AGVs. One potential direction for further research is route optimization, which could improve the efficiency of the AGV and overall system performance. Additionally, optimizing material flow in processes involving AGVs could also be explored. Finally, efforts to simplify and streamline M2M communication could be pursued, which would make it easier to integrate AGVs with existing industrial equipment. Overall, this study contributes to the field of industrial automation and highlights the potential for AGVs and M2M communication to improve efficiency and productivity in industrial settings.

## Future improvements

Future improvements include incorporating more industrial machinery into the framework and utilising the framework in a real (limited) industrial setting. That is, the AGV could actually accomplish specific tasks and simultaneously guide industrial machinery in real time. Furthermore, incorporating more AGVs to broaden the range of a singular AGV could be explored.
