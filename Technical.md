# AI Core Backend

## Models and Algorithms

| Function         | Model               |
|------------------|---------------------|
| Face Detection   | Yunet from OpenCV   |
| Face Recognition | SFace from OpenCV   |
| Tracker          | SORT Tracker        |

## Overview

On the server side, we use RTSP to obtain the camera feed and process the video frames. In each frame, we detect faces and update the tracker to differentiate between newly detected faces and those already tracked.

For new faces, we utilize the recognition model to extract feature vectors and proceed to the searching phase. In this phase, we use KNN to identify the five most similar but distinct faces.

Each tracked face has a `last recognition attempt counter` to re-identify the face, mitigating false identifications by ultimately selecting the highest score.

When a face exits the frame, we save its record (name, time seen, face image) to the server, which then stores it in the database.

## Technologies

We use C++ with OpenCV for the computer vision components.

# Server

The server manages communication between the AI Core, web app, mobile app, and database. We use Protocol Buffers for communication between the server and these components. The server is written in C++ and interacts with the database using nanodbc.
