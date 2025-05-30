Rapport : Mise en œuvre, Déploiement, Test et Consommation d’un Web Service SOAP avec JAX-WS – Présenté par M. Mohamed Youssfi

Introduction
Cette vidéo didactique détaille le développement d’un service web SOAP (Simple Object Access Protocol) autour d’une application bancaire simplifiée. Ce service expose des fonctionnalités comme la conversion de devises et la gestion de comptes. L’objectif est de concevoir un service SOAP en Java, de le tester via SoapUI, puis de générer et exploiter les classes Java à partir du fichier WSDL correspondant.

Lien vers la vidéo : https://www.youtube.com/watch?v=WZi3s2bZNAE

Architecture du Projet
1. Organisation des fichiers
Le projet suit la structure typique d’un projet Maven :

src/main/java : Dossier contenant le code source principal.

ws : Package regroupant les classes du service web.

BanqueService.java : Définit les opérations disponibles via le service.

Compte.java : Représente l'entité "Compte bancaire".

ServerJWS.java : Démarre et publie le serveur SOAP.

src/main/resources : Dossier pour les ressources annexes.

target : Généré automatiquement après la compilation.

pom.xml : Fichier de configuration Maven (dépendances, plugins, etc.).

2. Fichiers clés
ServerJWS.java : Point d’entrée du serveur SOAP, utilisant jakarta.xml.ws.Endpoint pour exposer le service sur http://0.0.0.0:9090/.

java
Copier
Modifier
Endpoint.publish(url, new BanqueService());
System.out.println("Serveur lancé sur " + url);
BanqueService.java : Contient les méthodes métiers annotées avec @WebService.

conversion(double mt) : Convertit un montant d’euros en dirhams marocains (taux fixe ×11).

getCompte(int code) : Récupère un compte à partir de son identifiant.

listComptes() : Retourne une liste de comptes simulés.

Compte.java : Modélise les comptes bancaires avec des attributs comme le solde, le code et la date de création.

3. Module client : client-soap-java
Ce module Maven est dédié au client SOAP.

Package principal : net.bousmara.clientsoapjava

Fichier principal : Main.java, qui constitue le point d’exécution.

Classes générées automatiquement via "Generate Java from WSDL" ou wsimport :

BanqueService.java

BanqueWS.java

Compte.java

Étapes de Développement
1. Création du service SOAP
La classe BanqueService est annotée avec @WebService pour signaler qu’il s’agit d’un service SOAP. Chaque méthode publique est exposée avec l’annotation @WebMethod, et les paramètres sont nommés via @WebParam.

2. Publication du serveur
Le service est publié grâce à Endpoint.publish(), le WSDL étant ensuite accessible via l’URL suivante :

arduino
Copier
Modifier
http://localhost:9090/BanqueWS?wsdl
3. Tests à l’aide de SoapUI
Après lancement du serveur, l’application SoapUI permet de valider les opérations du service :

conversion : pour tester la conversion d’euros en dirhams.

getCompte : pour récupérer les données d’un compte.

listComptes : pour consulter une liste aléatoire de comptes bancaires.

4. Génération des classes Java à partir du WSDL
À l’aide d’Eclipse ou de l’outil wsimport, on génère les classes proxy nécessaires à la consommation du service côté client :

Les interfaces pour les appels distants.

Les entités comme Compte.

Les stubs et classes utilitaires (BanqueService, BanqueWS, etc.).

Parmi les méthodes disponibles dans le client :

conversionEuroToDH(double mt) : Conversion d’une somme en dirhams.

getCompte(int code) : Récupération des données d’un compte spécifique.

listComptes() : Affichage de la liste des comptes renvoyée par le serveur.
Captures d'écran :
![2](https://github.com/user-attachments/assets/f7416720-db20-4eaa-be4e-4c82bbde939f)
![3](https://github.com/user-attachments/assets/df391619-2b02-4642-94d0-ad1dc2814029)
![4](https://github.com/user-attachments/assets/36c5caae-d6e9-4da8-97c2-ea7518fd2845)
![5](https://github.com/user-attachments/assets/54aa2db6-97cf-4db6-bb18-66fd6596861d)
![6](https://github.com/user-attachments/assets/e2a4adf7-9c55-43a8-ab85-50818904cf77)
![7](https://github.com/user-attachments/assets/4296de3d-92f7-42c7-9314-b809bfd8d62c)


