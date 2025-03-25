# Home Dashboard

## 📌 Description
Ce projet est un **Home Dashboard** conçu pour être affiché sur un écran connecté à une **Raspberry Pi 3B**. Il permet d'afficher **la météo, un calendrier (iCal), et des flux RSS** dans une interface moderne et esthétique.

L'architecture repose sur :
- **Frontend** : Vue.js (affichage des données)
- **Backend** : Flask (API pour récupérer et traiter les données)
- **MQTT** : Communication temps réel entre le backend et le frontend
- **Base de données** : SQLite ou Redis (stockage temporaire des informations)

## 🚀 Objectifs
- Développement sur un **PC** avant déploiement sur la **Raspberry Pi**.
- Démarrage automatique sur la Raspberry Pi avec affichage en plein écran.
- Communication en **temps réel** via MQTT.

## 🏗️ Plan de Développement

### **1️⃣ Mise en place de l’environnement**
1. Installer **Docker** sur le PC.
2. Créer un dépôt **Git** pour versionner le projet.
3. Configurer un fichier **docker-compose.yml** pour orchestrer les services.

### **2️⃣ Développement du backend (Python + Flask)**
4. Initialiser un projet Flask et créer une API REST.
5. Ajouter une route `/ping` pour tester l'API.
6. Implémenter la récupération des **données météo** via une API externe.
7. Ajouter la gestion du **calendrier (iCal)**.
8. Intégrer un **parser RSS** pour afficher des flux d’actualités.
9. Mettre en place **Flask-MQTT** pour envoyer des mises à jour en temps réel.
10. Utiliser **SQLite ou Redis** pour stocker temporairement les données.
11. Tester le backend avec **Postman** ou **cURL**.

### **3️⃣ Développement du frontend (Vue.js + UI)**
12. Initialiser un projet Vue.js avec **Vite**.
13. Ajouter **Vue Router** pour la navigation.
14. Utiliser **Vuetify, Tailwind CSS ou Bootstrap** pour un design moderne.
15. Concevoir une **maquette du dashboard**.
16. Intégrer les appels API Flask (`fetch` ou `axios`).
17. Ajouter **MQTT.js** pour la communication en temps réel.

### **4️⃣ Tests et Intégration sur PC**
18. Vérifier que le frontend affiche bien les données météo, calendrier et RSS.
19. Tester la communication **MQTT** entre backend et frontend.
20. Simuler un environnement Raspberry Pi pour tester les performances.

### **5️⃣ Déploiement sur Raspberry Pi**
21. Installer **Raspberry Pi OS** et Docker.
22. Copier le projet sur la Raspberry Pi et tester avec `docker-compose up`.
23. Optimiser les performances (caching, allègement des requêtes API).
24. Configurer l’**autostart** pour le backend et le broker MQTT.
25. Configurer **Chromium en mode kiosk** pour afficher l’interface au démarrage.

### **6️⃣ Optimisation et Améliorations**
26. Ajouter des **logs et gestion des erreurs**.
27. Optimiser les **requêtes API** pour réduire la charge.
28. Améliorer le **design** et ajouter des **animations**.
29. Tester plusieurs **brokers MQTT** pour la meilleure performance.
30. Ajouter des **fonctionnalités supplémentaires** (horloge, capteurs IoT, domotique).

## 📂 Architecture du Projet
```
/home-dashboard/
│── backend/       # API Flask (Python)
│── frontend/      # Interface Vue.js
│── mqtt/          # Broker MQTT (Mosquitto)
│── docker-compose.yml  # Configuration Docker
│── README.md      # Documentation du projet
```

## 🛠️ Technologies Utilisées
- **Backend** : Flask, SQLite/Redis, Flask-MQTT
- **Frontend** : Vue.js, Vuetify/Tailwind CSS, MQTT.js
- **Communication** : MQTT (Mosquitto)
- **Déploiement** : Docker, Raspberry Pi OS

## 📢 Démarrage du Projet (PC)
1. Cloner le projet :
   ```bash
   git clone https://github.com/ton-repo/home-dashboard.git
   cd home-dashboard
   ```
2. Lancer les services avec Docker :
   ```bash
   docker-compose up -d
   ```
3. Accéder à l'interface :
   - Backend : `http://localhost:5000`
   - Frontend : `http://localhost:8080`

## 🔥 Déploiement sur Raspberry Pi
1. Copier le projet sur la Raspberry Pi.
2. Lancer Docker :
   ```bash
   docker-compose up -d
   ```
3. Vérifier que l'interface s'affiche en plein écran.

---

🎯 **Prochaines étapes** : Ajout de fonctionnalités et optimisation des performances.

💡 **Idées ou suggestions ?** Ouvre une issue sur GitHub ! 🚀

