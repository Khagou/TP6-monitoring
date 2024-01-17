# TP6 Mise en place d’une solution de supervision d’applications contenerisées basées sur prometheus et grafana

## Contexte et composition du repot

Il est demande de mettre en place une solution de monitoring centralié pour stocker les métriques et fournir des tableaux de bord de surveillance.

L'ensemble du repot permet de déployer Elastic Cloud for Kubernetes sur un cluster GKE.

Le repot est composé de 1 dossier:
- Le fichier **ingress** sert à exposer grafana
- Le fichier **fleet.yml** qui déploie elastic, kibana, fleet et nginx
  - d'un fichier **cloudbuild.yml** qui permets de lancer le déploiement avec cloudbuild
- Le script **prod.sh** qui ce connecte au cluster, ajoute les droits au compte de service **<numero_de_projet>@cloudbuild.gserviceaccount.com** et lance le deploiement de ECK et Nginx

## Prerequis

- Disposer d'un compte de facturation GCP
- Disposer d'un cluster avec des nodes sur des type de machines e2-standard-2
- Disposer d'un bucket
- Avoir activé l'API cloudbuild



### Deploiement

  - Accéder à Cloud Shell et cloner le repot
  - Ouvrir l'éditeur et modifier l'ensemble des variable du script **prod.sh**
  - DAns le fichier cloudbuild.yml modifier la location et le cluster
  - Ouvrir un terminal dans l'editeur et lancer la commande 
      ```
      sh prod.sh
      ```
  - Dans la console GCP accéder aux charges de travail de votre cluster et attendez que tout les **Etat** soient vert
  - Lancez maintenant la commande suivatent pour recupérer le mot de passe pour accéder à Kibana
      ```
      kubectl get secret elasticsearch-quickstart-es-elastic-user -o=jsonpath='{.data.elastic}' | base64 --decode; echo
      ```
  - Dans vos charges de travail ouvrez la suivante ***kibana-quickstart-kb*** et dans la section **Services associés** cliquez sur le point de terminaison, 
     une nouvelle page s'ouvre avec une erreur cette page ne fonctionne pas rajouter https:// au debut de l'url tel que par exemple **https://34.16.25.221:5601/**.
  - Identifiant Kibana
      user: elastic
      mdp: le mot de passe que vous avez recupéré précédemment
