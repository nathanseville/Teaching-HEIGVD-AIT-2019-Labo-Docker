---
title: "Rapport AIT - Lab04 - Docker"
author: [Nathan Séville, Julien Quartier]
titlepage: true
titlepage-color: "FFFFFF"
toc-own-page: true
toc-title: "Table des matières"
---



# Introduction



# Tasks

## Task 0: Identify issues and install the tools

> **[M1]** Do you think we can use the current solution for a production environment? What are the main problems when deploying it in a production environment?

Non, cette solution n'est pas adaptée à un environnement de production. En cas d'arrêt inopiné de *node*, aucun monitoring, ni procédure automatique n'est configurée. En cas de grande charge, aucune stratégie de *scaling* n'est définie. L'ajout de nouveau *container* est compliquée dans l'infrastructure courante (CF. **M2**).



> **[M2]** Describe what you need to do to add new `webapp` container to the infrastructure. Give the exact steps of what you have to do without modifiying the way the things are done. Hint: You probably have to modify some configuration and script files in a Docker image.

///// To complete

1. Ajouter une *webapp* dans le fichier `docker-compose.yml`.
2. Ajouter une *node* dans le fichier de configuration de *haproxy*, `haproxy.cfg`.



> **[M3]** Based on your previous answers, you have detected some issues in the current solution. Now propose a better approach at a high level.



> **[M4]** You probably noticed that the list of web application nodes is hardcoded in the load balancer configuration. How can we manage the web app nodes in a more dynamic fashion?



> **[M5]** In the physical or virtual machines of a typical infrastructure we tend to have not only one main process (like the web server or the load balancer) running, but a few additional processes on the side to perform management tasks.
>
> For example to monitor the distributed system as a whole it is common to collect in one centralized place all the logs produced by the different machines. Therefore we need a process running on each machine that will forward the logs to the central place. (We could also imagine a central tool that reaches out to each machine to gather the logs. That's a push vs. pull problem.) It is quite common to see a push mechanism used for this kind of task.
>
> Do you think our current solution is able to run additional management processes beside the main web server / load balancer process in a container? If no, what is missing / required to reach the goal? If yes, how to proceed to run for example a log forwarding process?



> **[M6]** In our current solution, although the load balancer configuration is changing dynamically, it doesn't follow dynamically the configuration of our distributed system when web servers are added or removed. If we take a closer look at the `run.sh` script, we see two calls to `sed` which will replace two lines in the `haproxy.cfg` configuration file just before we start `haproxy`. You clearly see that the configuration file has two lines and the script will replace these two lines.
>
> What happens if we add more web server nodes? Do you think it is really dynamic? It's far away from being a dynamic configuration. Can you propose a solution to solve this?



**Deliverables**

1. ![HAProxy Stat](img/T0_haproxystat.png)
2. https://github.com/nathanseville/Teaching-HEIGVD-AIT-2019-Labo-Docker



## Task 1: Add a process supervisor to run several processes

**Deliverables**

1. ![HAProxy Stat Backend](img/T1_haproxystat.png)
2. L'installation d'un *process supervisor* tel que `S6` va nous permettre de lancer plusieurs processus par *container* `docker`, c'est important qu'on puisse le faire afin de pouvoir ajouter par exemple un processus qui communique sur l'état de la *node* pour pouvoir les manager correctement en fonction de leur état.

// TO COMPLETE



## Task 2: Add a tool to manage membership in the web server cluster

1. Les logs sont dans le dossier `logs` à la racine du git.
2. Le problème c'est que notre `Serf` sur le HAProxy ne prend pas en charge la gestion des membres de `Serf`.
3. /// TO COMPLETE



## Task 3: React to membership changes



# Difficulties



# Conclusion

