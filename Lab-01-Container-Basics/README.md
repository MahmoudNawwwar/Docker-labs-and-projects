

# Lab 01 - Docker Container Basics

## Overview

This lab covers the fundamental Docker container operations including:

- Creating containers
- Starting containers
- Executing commands inside containers
- Inspecting containers
- Stopping containers
- Removing containers
- Understanding Images vs Containers
- Common Docker troubleshooting scenarios

---

# Objectives

After completing this lab, you will be able to:

- Understand Docker Images and Containers
- Create Docker containers
- Start and stop containers
- Execute commands inside running containers
- Inspect container details
- Remove containers safely
- Force remove running containers
- Troubleshoot common Docker issues

---

# Prerequisites

- Linux Operating System
- Docker Installed
- Internet Connection

Verify Docker Installation:

```bash
docker --version
```

---

# Section 1: Docker Fundamentals

## Question 1

What is Docker?

### Answer

Docker is a containerization platform used to package applications and their dependencies into lightweight and portable containers.

---

## Question 2

What is a Docker Image?

### Answer

A Docker Image is a read-only template used to create containers.

Example:

```text
nginx image
ubuntu image
alpine image
```

---

## Question 3

What is a Docker Container?

### Answer

A Docker Container is a running instance of a Docker Image.

Example:

```text
Image  --->  Container

nginx  --->  web-server
ubuntu --->  dev-server
```

---

## Question 4

What is the difference between an Image and a Container?

### Answer

| Image | Container |
|---------|---------|
| Template | Running Instance |
| Read Only | Writable |
| Static | Dynamic |
| Used to Create Containers | Created From Images |

---

## Question 5

Display all downloaded images.

### Answer

```bash
docker images
```

---

## Question 6

Display running containers.

### Answer

```bash
docker ps
```

---

## Question 7

Display all containers.

### Answer

```bash
docker ps -a
```

---

# Section 2: Create Containers

## Question 8

Create a container named web-server using nginx image without starting it.

### Answer

```bash
docker create --name web-server nginx
```

---

## Question 9

Create a container named linux-tester using alpine image without starting it.

### Answer

```bash
docker create --name linux-tester alpine sleep 3600
```

---

## Question 10

Verify container creation.

### Answer

```bash
docker ps -a
```

Expected Output:

```text
STATUS
Created
```

---

## Question 11

What is the difference between docker create and docker run?

### Answer

docker create:

- Creates a container only

docker run:

- Creates and starts a container

Example:

```bash
docker create nginx
```

```bash
docker run nginx
```

---

# Section 3: Start Containers

## Question 12

Start web-server container.

### Answer

```bash
docker start web-server
```

---

## Question 13

Start linux-tester container.

### Answer

```bash
docker start linux-tester
```

---

## Question 14

Start both containers using a single command.

### Answer

```bash
docker start web-server linux-tester
```

---

## Question 15

Verify running containers.

### Answer

```bash
docker ps
```

Expected Output:

```text
STATUS
Up
```

---

# Section 4: Execute Commands Inside Containers

## Question 16

Display running processes inside web-server container.

### Answer

```bash
docker top web-server
```

---

## Question 17

Open an interactive shell inside linux-tester container.

### Answer

```bash
docker exec -it linux-tester sh
```

---

## Question 18

Create a directory named /app inside linux-tester.

### Answer

```bash
docker exec linux-tester mkdir /app
```

---

## Question 19

Create a file inside /app.

### Answer

```bash
docker exec linux-tester touch /app/file.txt
```

---

## Question 20

Verify file creation.

### Answer

```bash
docker exec linux-tester ls /app
```

Expected Output:

```text
file.txt
```

---

## Question 21

What is docker exec?

### Answer

docker exec runs a new process inside a running container.

Example:

```bash
docker exec -it linux-tester sh
```

---

## Question 22

What is the difference between docker exec and docker attach?

### Answer

docker exec:

- Starts a new process

docker attach:

- Attaches to the main running process

---

# Section 5: Inspect Containers

## Question 23

Inspect web-server container.

### Answer

```bash
docker inspect web-server
```

---

## Question 24

Inspect linux-tester container.

### Answer

```bash
docker inspect linux-tester
```

---

## Question 25

Display Container ID.

### Answer

```bash
docker inspect -f '{{.Id}}' web-server
```

---

## Question 26

Display Image Name.

### Answer

```bash
docker inspect -f '{{.Config.Image}}' web-server
```

---

## Question 27

Display Container Status.

### Answer

```bash
docker inspect -f '{{.State.Status}}' web-server
```

---

# Section 6: Stop Containers

## Question 28

Stop web-server container.

### Answer

```bash
docker stop web-server
```

---

## Question 29

Stop linux-tester container.

### Answer

```bash
docker stop linux-tester
```

---

## Question 30

Verify container status.

### Answer

```bash
docker ps -a
```

Expected Output:

```text
Exited
```

---

# Section 7: Remove Containers

## Question 31

Delete linux-tester container.

### Answer

```bash
docker rm linux-tester
```

---

## Question 32

Delete web-server container.

### Answer

```bash
docker rm web-server
```

---

## Question 33

Force remove a running container.

### Answer

```bash
docker rm -f web-server
```

---

## Question 34

What is the difference between rm and rm -f?

### Answer

docker rm

- Removes stopped containers only

docker rm -f

- Stops and removes running containers

---

# Interview Questions

## Question 35

What happens if the Docker Engine restarts?

### Answer

Containers restart only if a restart policy is configured.

Example:

```bash
docker run --restart always nginx
```

---

## Question 36

Why does a container stop immediately after starting?

### Answer

Because the main process (PID 1) exits.

---

## Question 37

What keeps the alpine container running in this lab?

### Answer

The command:

```bash
sleep 3600
```

remains running and becomes PID 1.

---

## Question 38

What is PID 1 inside a container?

### Answer

PID 1 is the main process responsible for keeping the container alive.

---

# Common Errors and Troubleshooting

## Error 1

```bash
docker start linux-tester
```

Output:

```text
No such container
```

### Cause

Incorrect container name.

---

## Error 2

```bash
docker exec linux-tester cd /app
```

Output:

```text
executable file not found
```

### Cause

cd is a shell built-in command.

### Correct Method

```bash
docker exec -it linux-tester sh
```

Then:

```bash
cd /app
```

---

## Error 3

```bash
docker rm web-server
```

Output:

```text
cannot remove container
```

### Cause

Container is still running.

### Solution

```bash
docker rm -f web-server
```

---

# Lab Summary

In this lab we learned:

- Docker Images
- Docker Containers
- Creating Containers
- Starting Containers
- Executing Commands
- Inspecting Containers
- Stopping Containers
- Removing Containers
- Force Removing Containers
- Docker Troubleshooting
- Docker Interview Questions

---

# Author

Mahmoud Ali Nawwar

DevOps Engineer Learning Journey 🚀
