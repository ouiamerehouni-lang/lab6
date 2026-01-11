# lab6
**Etape 1: Préparer l’environnement Kubernetes**

On a mis en place un mini-cluster Kubernetes local et créé un espace isolé (churn-mlops) pour déployer notre système MLOps, prêt à accueillir les applications et services.

<img width="970" height="300" alt="image" src="https://github.com/user-attachments/assets/42ce06c6-aae0-4c11-9668-5f9e67b5c501" />
<img width="700" height="216" alt="image" src="https://github.com/user-attachments/assets/2c2a7e8e-b66a-45de-a1fc-bc5a4a2dd9c4" />
<img width="1245" height="127" alt="image" src="https://github.com/user-attachments/assets/f933ae8f-c009-4f40-ae31-729ea580c57b" />


**Étape 2 : Préparer l’image Docker de l’API churn**

On a préparé un environnement Python isolé avec la version 3.12 et installé toutes les dépendances nécessaires pour que l’API churn fonctionne correctement

<img width="612" height="55" alt="image" src="https://github.com/user-attachments/assets/06c4916d-aa03-4839-91bc-6c4477d4eac5" />
<img width="1064" height="154" alt="image" src="https://github.com/user-attachments/assets/575abc76-b913-4be0-b3d0-3bb25c6f9062" />
<img width="874" height="272" alt="image" src="https://github.com/user-attachments/assets/8e213dde-2d8f-401f-9e57-24bb9faa7146" />


**Étape 3 : Créer le dossier des manifests Kubernetes**

On a créé un dossier k8s pour y mettre tous les manifests Kubernetes (fichiers de configuration pour déployer les pods, services, etc...), afin de préparer l’organisation du projet pour le déploiement.
<img width="917" height="224" alt="image" src="https://github.com/user-attachments/assets/c43b3ba5-139f-4db5-84f3-0fe1d46cadbf" />
<img width="758" height="705" alt="image" src="https://github.com/user-attachments/assets/5457f99e-50ed-40e2-a8b3-11d3006aac44" />


**Étape 4 : Construire l’image Docker (tag versionné)**

On a construit l’image Docker de l’API churn avec un tag versionné (v1) pour pouvoir la déployer dans Kubernetes, et on a vérifié qu’elle existe bien sur la machine locale.

<img width="1308" height="356" alt="image" src="https://github.com/user-attachments/assets/9b518946-9c1e-4524-9977-49caad174633" />
<img width="1287" height="177" alt="image" src="https://github.com/user-attachments/assets/87827229-b02b-4a22-8a9e-75a9404d632f" />


**Étape 5 : Charger explicitement l’image dans Minikube**


On a transféré l’image Docker churn-api:v1 dans Minikube afin que Kubernetes puisse créer des pods sans dépendre d’un registre externe.
<img width="1298" height="259" alt="image" src="https://github.com/user-attachments/assets/c14a8879-a395-4275-97c9-0bfd3bfb33e6" />


**Étape 6 : Deployment Kubernetes pour l’API churn**

On a déployé l’API churn dans Kubernetes en créant un Deployment qui lance deux réplicas de l’application à partir de l’image Docker churn-api:v1. On a ainsi assuré que l’API fonctionne de manière continue, avec plusieurs Pods gérés automatiquement par Kubernetes.

<img width="854" height="600" alt="image" src="https://github.com/user-attachments/assets/7c81ab06-67d5-42d9-bdbb-c4f56906259b" />
<img width="933" height="279" alt="image" src="https://github.com/user-attachments/assets/d788228d-cd19-4dd5-bdef-bfd256eaf1b6" />


**Étape 7 : Exposer l’API via un Service NodePort**

On a rendu l'application accessible à l'extérieur du cluster en configurant un Service NodePort, créant ainsi un point d'accès stable sur le port 30080. Ce service fait le lien entre les requêtes externes et le port 8000 de nos conteneurs.
On a ensuite validé le bon fonctionnement de l'ensemble du système en envoyant une requête JSON à FastAPI. Cette étape a permis de confirmer que l'infrastructure Kubernetes redirige correctement les données vers le modèle de Machine Learning et que celui-ci renvoie une prédiction valide en temps réel, garantissant ainsi la disponibilité opérationnelle de l'API.

<img width="425" height="453" alt="image" src="https://github.com/user-attachments/assets/cdb88144-844a-4d6f-82b4-547d9306c7fb" />
<img width="865" height="346" alt="image" src="https://github.com/user-attachments/assets/58bdbf36-e78d-4737-a779-c920ef8c5d71" />
<img width="925" height="372" alt="image" src="https://github.com/user-attachments/assets/e4c711a7-a6b1-4f29-820f-93061596f36e" />


**Étape 8 : Injecter la configuration MLOps via ConfigMap**

On a ajouté une configuration externe à l’API via un ConfigMap Kubernetes, ce qui permet de changer le nom du modèle et le niveau de logs sans modifier le code ni l’image Docker.
<img width="833" height="330" alt="image" src="https://github.com/user-attachments/assets/3d29d3c2-8a18-425a-9793-7a487952a65c" />
<img width="864" height="663" alt="image" src="https://github.com/user-attachments/assets/76f3e711-2b5c-4ae4-aeb0-6a47b1cd5c7a" />
<img width="913" height="103" alt="image" src="https://github.com/user-attachments/assets/899db95f-4012-4f8e-94f5-1b6986192a5a" />
<img width="923" height="207" alt="image" src="https://github.com/user-attachments/assets/8872a5ba-ee97-4dd6-9a32-5b6041d16a70" />


**Étape 9 : Gérer les secrets (MONITORING_TOKEN)**

On a sécurisé les informations sensibles en créant un Secret Kubernetes. Contrairement au ConfigMap, cet objet permet de stocker des données confidentielles, comme le jeton MONITORING_TOKEN, en utilisant un encodage Base64 pour éviter l'affichage en clair dans les fichiers de configuration.
On a ensuite intégré ce secret dans le Deployment afin qu'il soit injecté comme variable d'environnement dans les Pods.

<img width="846" height="648" alt="image" src="https://github.com/user-attachments/assets/04481ab6-006e-4290-b5f7-fd7d8d64f63d" />
<img width="927" height="250" alt="image" src="https://github.com/user-attachments/assets/a0ea8b12-0ab8-4e6f-bed8-6648d4ba22cd" />

**Étape 10 : Mise en place des endpoints de santé et des probes Kubernetes pour l’API Churn**

On a rendu l’API Churn observable et robuste en ajoutant des endpoints de santé dédiés, afin que Kubernetes puisse vérifier automatiquement que l’application est prête à recevoir du trafic et qu’elle fonctionne normalement. Ensuite, on a reconstruit et redéployé l’image Docker pour que ces nouveaux endpoints soient pris en compte par le cluster Minikube.

<img width="922" height="281" alt="image" src="https://github.com/user-attachments/assets/b2f46597-c1b5-41fa-9334-f6adc132e861" />
<img width="906" height="59" alt="image" src="https://github.com/user-attachments/assets/cbb41ba4-1481-4642-87f1-1105a66b44ec" />



**Étape 11 : Ajouter les probes (liveness / readiness / startup)**

On a appris à Kubernetes comment surveiller automatiquement l’état de l’API Churn en configurant des probes de santé.
Kubernetes sait quand l’application a correctement démarré, quand elle est prête à recevoir du trafic

<img width="916" height="581" alt="image" src="https://github.com/user-attachments/assets/e7541864-aaa5-4639-a912-984a4bfc892a" />
<img width="925" height="447" alt="image" src="https://github.com/user-attachments/assets/7345bdc8-86fc-4afc-a960-044010399dc0" />



**Étape 12 : Volume persistant pour registry + logs**

On a mis en place un stockage persistant pour sécuriser les modèles et les logs de l’API Churn.
Concrètement, on a créé un volume persistant (PVC) pour conserver les fichiers même si les Pods Kubernetes sont supprimés ou redémarrés. On a ensuite utilisé un Job Kubernetes pour entraîner un premier modèle et l’enregistrer directement dans ce volume.

<img width="928" height="453" alt="image" src="https://github.com/user-attachments/assets/e6533eb9-a8f9-40c1-94f7-52f94fd19d43" />
<img width="930" height="400" alt="image" src="https://github.com/user-attachments/assets/73b5e3ab-7ed4-4aab-8d63-58fc549baa9c" />
<img width="932" height="329" alt="image" src="https://github.com/user-attachments/assets/8ff2d311-a5c3-45a7-8b55-132a37f6ee75" />


**Étape 13 : NetworkPolicy**

On a défini une règle réseau pour contrôler qui peut accéder à l’API Churn à l’intérieur du cluster Kubernetes.
Grâce à la NetworkPolicy, on autorise uniquement le trafic entrant provenant d’autres Pods du cluster vers les Pods churn-api, et seulement sur le port 8000. Tout autre trafic entrant est implicitement bloqué.

<img width="904" height="397" alt="image" src="https://github.com/user-attachments/assets/6ea332ed-ce12-40d3-8b02-cf81b1555a93" />


