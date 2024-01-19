# TP6 Mise en place d’une solution de supervision d’applications contenerisées basées sur prometheus et grafana sur GCP

## Contexte et composition du repot

Il est demande de mettre en place une solution de monitoring centralié pour stocker les métriques et fournir des tableaux de bord de surveillance.

L'ensemble du repot permet de déployer Elastic Cloud for Kubernetes sur un cluster GKE.

Le repot est composé de 1 dossier:
- Le fichier **ingress** sert à exposer grafana
- Le fichier **mysql.yml** qui déploie MySQL
- Le fichier **nginx.yml** qui permets de déployer nginx

## Prerequis

- Disposer d'un compte de facturation GCP
- Disposer d'un cluster 


## Deploiement

  - Accéder à Cloud Shell et cloner le repot
  - Si ce n'est pas déjà fait, ce connecter au cluster
  - Puis lancer la commande
      ```
      helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
      helm repo update
      ```
  - Lancez maintenant la commande suivate pour installer prometheus
      ```
      helm install [RELEASE_NAME] prometheus-community/kube-prometheus-stack
      ```
  - Dans vos charges de travail ouvrez la suivante ***<release_name>-grafana*** et dans la section **Services associés** cliquez sur le point de terminaison, 
     une nouvelle page s'ouvre et affiche le menu de connexion de grafana.
  - Identifiant Grafana
      user: admin
      mdp: prom-operator
  - Une fois connecté accédez au menu dashboard, vous constaterez alors la présence de nombreux dashboards offrant de nombreuses metrics sur votre cluster, vos noeuds, pods ...
    Si vous accédez maintenant au menu Alerting vous constaterez la présence de nombreuses alertes pré-configuré. 
    Vous pouvez biensur personnaliser les alertes et les dashboards.
