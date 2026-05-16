# TP Zabbix

Ce TP a pour objectif de mettre en place une supervision de base avec Zabbix sur une VM Linux, puis de créer plusieurs éléments de supervision, un déclencheur et une réflexion autour de la supervision de système de fichiers et de la notification par mail.[cite:138]

## Objectifs pédagogiques

À la fin de ce TP, il doit être possible de :

- Installer et configurer l’agent Zabbix sur une machine Linux.[cite:138]
- Déclarer un hôte dans l’interface Zabbix.[cite:138]
- Créer des items pour superviser la connectivité, le temps de réponse, la RAM, le CPU, Apache, Postgres et un système de fichiers.[cite:138]
- Consulter les dernières données et les représentations graphiques dans l’interface de supervision.[cite:138]
- Mettre en place un déclencheur en cas d’arrêt du service Apache.[cite:138]
- Tester le comportement de la supervision et envisager une extension avec notification mail.[cite:138]

## Prérequis

Avant de commencer, les éléments suivants doivent être disponibles :

- Une VM Linux accessible en ligne de commande.[cite:138]
- Les droits nécessaires pour installer des paquets et redémarrer des services.[cite:138]
- Un accès au serveur Zabbix via le navigateur avec l’URL et les identifiants fournis dans le TP.[cite:138]
- L’adresse IP de la machine à superviser pour l’ajout de l’interface de type agent dans Zabbix.[cite:138]

## Contenu du TP

Le TP suit la progression suivante :

| Étape | Sujet | Description |
|---|---|---|
| 1 à 3 | Installation agent | Installation de `zabbix-agent`, modification du fichier `zabbix_agentd.conf`, puis redémarrage du service.[cite:138] |
| 4 à 5 | Déclaration de l’hôte | Connexion à l’interface Zabbix puis création d’un nouvel hôte dans le groupe `serveurs linux`.[cite:138] |
| 6 à 8 | Connectivité | Création d’un item `agent.ping`, d’un item `icmppingsec`, puis consultation des dernières données.[cite:138] |
| 9 à 12 | Supervision système | Création d’items pour la RAM, le CPU, Apache, Postgres et un système de fichiers.[cite:138] |
| 13 à 15 | Déclencheur | Configuration d’un trigger Warning lors de l’arrêt d’Apache, test, puis validation du retour à l’état normal.[cite:138] |
| 16 à 17 | Réflexion | Supervision avancée d’un FS sur LVM avec seuil à 80% et configuration d’une notification mail.[cite:138] |

## Paramètres utilisés

Les paramètres de configuration explicitement demandés dans le TP sont les suivants :

```bash
sudo apt install zabbix-agent
sudo vim /etc/zabbix/zabbix_agentd.conf

AllowKey=system.run[*]
Server=172.16.2.49
ServerActive=172.16.2.49
Hostname=VotreNom-server

sudo systemctl restart zabbix-agent
```

Ces commandes et valeurs correspondent à la phase d’installation et de configuration de l’agent dans le document du TP.[cite:138]

## Accès à l’interface Zabbix

Le TP demande d’accéder à l’interface web Zabbix via l’URL suivante, avec un compte `adminX` et le mot de passe fourni dans l’énoncé.[cite:138]

- URL : `http://infra.efi-academy.com:3312/zabbix/`[cite:138]
- Utilisateur : `adminX` avec `X` correspondant au numéro de l’apprenant.[cite:138]
- Mot de passe : `zabbix@2023`.[cite:138]

## Items à créer

Les principaux items demandés dans le TP sont résumés ci-dessous :

| Nom | Type | Clé | Type d’information | Intervalle |
|---|---|---|---|---|
| verif ping | agent Zabbix | `agent.ping` | — | 10s [cite:138] |
| temps de reponse ping | Verification simple | `icmppingsec` | — | 10s [cite:138] |
| Utilisation RAM | agent Zabbix | `vm.memory.size[pused]` | Numérique (flottant) | 10s [cite:138] |
| Utilisation CPU | agent Zabbix | `system.cpu.util` | Numérique (flottant) | 5s [cite:138] |
| Service apache | agent Zabbix | `system.run[systemctl is-active apache2]` | Chaine | 20s [cite:138] |
| Service postgres | agent Zabbix | `proc.num[postgres]` | Numérique (entier) | 20s [cite:138] |
| FS | agent Zabbix | `system.run[ ??????????????]` | Numérique (flottant) | 20s [cite:138] |

## Partie déclencheur

Le TP demande de configurer un déclencheur générant un événement de niveau Warning lorsque le serveur Apache s’arrête, puis de tester ce comportement en arrêtant et en relançant le service.[cite:138]

Cette étape permet de valider le cycle complet de supervision : collecte, détection d’un incident, remontée d’un événement, puis retour à un état sain.[cite:138]

## Travail de réflexion

La dernière partie du TP propose deux prolongements :

- Superviser un système de fichiers sur une machine LVM et créer un déclencheur lorsque le taux d’occupation dépasse 80%.[cite:138]
- Configurer une action de notification par mail en réponse au déclencheur.[cite:138]

Cette partie ouvre la voie vers une supervision plus réaliste orientée production, avec seuils d’alerte et mécanisme de notification.[cite:138]

## Remarques

- Le contenu du TP inclut une clé de supervision du FS laissée volontairement incomplète dans l’énoncé.[cite:138]
- Le README peut être utilisé comme page d’accueil du dépôt contenant le TP PDF et la version HTML designée.[cite:138]
- Ce document sert de guide d’accompagnement, sans modifier la structure pédagogique du TP original.[cite:138]
