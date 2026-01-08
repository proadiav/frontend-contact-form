README.md
Introduction

Ce projet met en place une mini-infrastructure d’agent IA auto-hébergée.

Concrètement, il permet :

d’afficher une interface web simple (frontend),

d’envoyer des données vers un backend automatisé,

de traiter ces données avec n8n,

de les stocker dans une base de données.

Le tout est hébergé sur une machine virtuelle Google Cloud, sécurisé en HTTPS, et orchestré avec Docker.

Architecture simplifiée (en mots simples)

L’utilisateur remplit un formulaire sur une page web.

Le formulaire envoie les données vers un webhook n8n.

n8n traite les données (logique métier).

Les données sont enregistrées dans Supabase.

n8n renvoie une réponse au frontend.

Prérequis

Avant de lancer le projet, il faut :

1. Un compte Google Cloud

Une VM Ubuntu 22.04 (type e2-micro).

Les ports suivants ouverts :

22 (SSH)

80 (HTTP)

443 (HTTPS)

2. Docker et Docker Compose

Docker permet de lancer les services sans installation manuelle complexe.

Sur la VM :

docker --version
docker compose version


Si ces commandes fonctionnent, Docker est prêt.

3. Accès SSH par clé

Connexion sécurisée au serveur.

Pas de mot de passe.

Pas de login root.

Déploiement du projet (pas à pas)
Étape 1 : Connexion au serveur
ssh user@IP_DE_LA_VM

Étape 2 : Cloner le dépôt GitHub
git clone https://github.com/TON_COMPTE/infra-n8n-antigravity.git
cd infra-n8n-antigravity

Étape 3 : Configuration des variables d’environnement

Créer le fichier .env à partir de l’exemple :

cp .env.example .env


Puis compléter les valeurs (domaines, ports, clés, etc.).

Étape 4 : Lancer l’infrastructure
docker compose up -d


Pour vérifier que tout tourne :

docker compose ps


Les services doivent être en état running.

Accès aux services

n8n :
https://n8n.tondomaine.com

Frontend :
Hébergé sur GitHub Pages

Description du flux de données

L’utilisateur remplit un formulaire sur la page frontend.

Le formulaire envoie une requête HTTP POST.

La requête contient :

des données (nom, email, message),

un header de sécurité (x-api-key).

n8n reçoit la requête via un webhook sécurisé.

n8n exécute un workflow :

traitement,

enregistrement dans Supabase.

n8n renvoie une réponse JSON.

Le frontend affiche un message de succès.

Sécurité mise en place

Accès SSH par clé uniquement.

HTTPS via reverse proxy.

Webhooks protégés par header (x-api-key).

Aucun service exposé inutilement.

Objectif pédagogique

Ce projet démontre :

la compréhension d’une architecture web moderne,

l’utilisation de Docker,

l’orchestration de services,

la communication frontend ↔ backend,

les bases de la sécurité serveur.
