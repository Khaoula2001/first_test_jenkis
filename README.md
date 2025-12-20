# TP 30 - Pipeline CI/CD avec Jenkins, GitHub, Docker et ngrok

Ce TP présente la mise en place d'une chaîne CI/CD complète automatisant le build, la conteneurisation avec Docker et le déploiement d'une application Spring Boot via un Pipeline Jenkins déclenché par des Webhooks GitHub exposés par ngrok.

---

## 1. Installation et première connexion à Jenkins
Jenkins a été installé et configuré sur le port 8080 avec les plugins recommandés.

![Dashboard Jenkins](screens/2025-12-19_10h00_08.png)

## 2. Configuration de Maven dans Jenkins
Configuration de l'outil Maven dans "Tools" pour permettre la compilation du projet.

![Configuration Maven](screens/2025-12-17_20h37_58.png)

## 3. Préparation du projet et Dockerfile
Vérification de la compilation locale et création du `Dockerfile` pour l'image de l'application.

![Build Maven Local 1](screens/2025-12-17_20h45_09.png)
![Build Maven Local Succès](screens/2025-12-17_20h45_14.png)

```dockerfile
FROM eclipse-temurin:17-jre
WORKDIR /App
COPY target/*.jar app.jar
EXPOSE 8282
ENTRYPOINT ["java","-jar","app.jar"]
```

## 4. Création et exécution du Pipeline Jenkins
Création d'un pipeline pointant vers GitHub avec les étapes : Git Clone, Build, Create Docker Image, et Run.

![Configuration Pipeline 1](screens/2025-12-19_09h09_48.png)
![Configuration Pipeline 2](screens/2025-12-19_09h09_56.png)
![Stage View](screens/2025-12-19_09h44_44.png)


## 5. Automatisation avec ngrok et Webhooks GitHub
Mise en place d'un tunnel ngrok pour exposer Jenkins et configuration du Webhook sur le dépôt GitHub.

![Setup ngrok](screens/2025-12-19_09h43_09.png)
![Auth ngrok](screens/2025-12-19_09h51_30.png)
![Tunnel ngrok actif](screens/2025-12-19_09h52_39.png)
![Webhook GitHub](screens/2025-12-19_11h12_05.png)
![URL Jenkins ngrok](screens/2025-12-19_11h21_59.png)

## 6. Test du déclenchement automatique (Git Push)
Validation finale : un `git push` déclenche instantanément le pipeline Jenkins via le Webhook.

![Git Push](screens/2025-12-19_11h27_50.png)
![Livraison Webhook réussie](screens/2025-12-19_11h30_05.png)
![Stage View Jenkins](screens/2025-12-19_11h50_44.png)
