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


On a copié l’image Docker de l’API churn dans l’environnement Minikube, afin que Kubernetes puisse l’utiliser pour créer les pods sans avoir besoin de la télécharger depuis un registre externe.



