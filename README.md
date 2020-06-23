# Bienvenido a  AWS ECS - Empezando de Cero

## Paso 1: Crear un cluster de ECS


create cluster
name: apache-cluster

## Paso 2: Crear "task definition"

create task definition
	name: httpd-container
	default type 


### Agregamos un contenedor oficial de Apache 2.4:

	add container
		container name: httpd-container
		image: httpd:2.4
		memory limits: 256
		port mappings: host port:80, container port: 80, tcp

### Parametros del contenedor adicionales:

	environment
		command:
    
>	/bin/sh -c "echo '<html> <head> <title>MY ECS first Demo</title><style>body {margin-top: 40px; background-color: #333;} </style> </head><body> <div style=color:white;text-align:center> <h1>Amazon ECS - Sample Web Server </h1> <h2>Congratulations!</h2> <p>You successfully set up your ECS cluster.</p> </div></body></html>' > /usr/local/apache2/htdocs/index.html && httpd-foreground"


## Creamos un IAM Role para el servicio ECS

create ecs role
	Switch to IAM.
	Click on “Roles” on the left side and then on “Create New Role”.
	Give your role a name, e.g. ecsInstanceRole.
	As a role type, select “Amazon EC2”.
	As a policy, attach “AmazonEC2ContainerServiceforEC2Role“.
	In the Review pane, click on “Create Role”

## Seleccionamos un host para nuestros contenedores

create ec2 -  amzn ami ecs optimized - community ami
	agregar instance role
	auto-assign public ip
	user data:
	#!/bin/bash
	echo ECS_CLUSTER=apache-cluster >> /etc/ecs/ecs.config

## Creamos un "service" en ECS

ECS - Create service

	service name: apache-service
	numnber of tasks: 1
	strategy: one task per host
	cluster vpc: 
	subnets
	sg
	auto assign : disable
	load balancer: none
	service discovery: none
  
  

