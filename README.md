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


<img width="833" height="330" alt="image" src="https://github.com/user-attachments/assets/3d29d3c2-8a18-425a-9793-7a487952a65c" />
<img width="864" height="663" alt="image" src="https://github.com/user-attachments/assets/76f3e711-2b5c-4ae4-aeb0-6a47b1cd5c7a" />
<img width="913" height="103" alt="image" src="https://github.com/user-attachments/assets/899db95f-4012-4f8e-94f5-1b6986192a5a" />

