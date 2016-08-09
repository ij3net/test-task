#!/bin/bash
#!!! Main part of test task in ansible subdirectory as playbook.

#This part create docker containers with installed supervisor and running ssh for using as testing targets.

git clone https://github.com/ij3net/test-task.git

cd ./test-task/pg_cluster

sudo docker compose up

#This part deploing requested configuration to configured invertory
cd ./ansible/

#Setup invertory

vi ./invertory

#Fill
vi ./defaults/main.yml

#Edit names to correspond previous.
vi ./role.yml

ansible-playbook -i inventory role.yml

