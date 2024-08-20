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

Industrial environments often face challenges in coordinating multiple machines due to limited space and scheduling constraints, leading to downtime and inefficiencies. M2M communication technology aims to facilitate autonomous interaction among smart devices, improving cost efficiency and time management without extensive integration efforts. AGVs, as mobile robots, offer a solution by autonomously transporting goods and utilizing sensor data for efficient navigation and task execution.

## Methods:

The case study involved a three-wheel differential drive AGV communicating with an overhead crane and an ultra-wideband radio signal system. The AGV used a 3D-lidar for navigation, and real-time measurements were integrated with a pre-measured point cloud map for accurate localization. Communication was established via HTTP requests and WebSocket protocols, enabling the AGV to interact with the crane for precise load positioning and maintaining a safety zone within the crane's operating area.

## Results:

The AGV successfully demonstrated M2M communication by accurately receiving the crane's hook position and initiating a safety zone. The reaction speed of the safety zone varied based on the placement of personnel tags, with mean reaction times of 12.92 seconds (waist) and 19.38 seconds (neck). The localization accuracy was within acceptable industrial ranges, validating the AGV's navigation capabilities.

## Discussion:

The study confirms the feasibility of using AGVs for M2M communication with industrial equipment, presenting a flexible solution for automation tasks. Future research directions include optimizing route efficiency, material flow processes, and simplifying M2M communication integration to enhance the overall performance and ease of implementation in industrial settings.
