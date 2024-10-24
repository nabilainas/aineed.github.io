---
title: "Déploiement d'une application web avec Azure Container Apps"
groupByYear: false
date: 2024-10-10
showComments: True
showTableOfContents:
  article: True
draft: true
---
{{< lead >}}
Intégration d'une application web dans une usine devops pour le déploiement continu
{{< /lead >}}

## Introduction

Dans le cadre de mes études, pour mon premier cours de M2 à [Sup De Vinci](https://www.supdevinci.fr/), nous avons eu pour objectif de déployer une application web dans le cloud, en privilégiant l'utilisation d'une approche DevOps concentrée sur le déploiement continu. 

Il y à une infinité de possiblités pour déployer une application, cependant, avec les contraintes imposées par le formateur et les potentiels point bonus on arrive à faire des choix

Concernant l'application en elle même, il n'y à pas de contraintes particulières etant donné que ce n'est pas le sujet principal de l'évaluation.
Cependant, On à des points bonus si on met en place du caching et des queues d'attente (Ce que l'on va faire, ceci est détaillé dans ce projet). 


Du côté du déploiement en lui même on nous encourage à :
- Provisionnement avec Terraform
- Configuration avec Ansible
- Monitoring avec Prometheus
- Visualisation avec Grafana
- Automatisation avec Jenkins, Gitlab CI ou Github Actions

et par rapport au bonus on à:
- Orchestration (Kubernetes) / Conteneurisation (Docker)
- Multi-cloud simultané
- Auto-scaling
- Backup / Disaster recovery


## Architecture

Voici l'architecture globale du projet :

### Workflow pipeline de déploiement

vous pouvez avoir accès à la totalité du code en public [ici](https://gitlab.com/webapp6384540/deploy/-/tree/main)