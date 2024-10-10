
# Projet de Migration Terraform vers OpenTofu

## Objectif

Ce projet vise à démontrer la faisabilité de la migration d'infrastructures gérées avec Terraform vers **OpenTofu**, suite au changement de licence de Terraform en 2023. Nous avons également mis en place une intégration continue (CI/CD) sur GitLab pour automatiser les étapes de validation et de déploiement de l'infrastructure.

## Structure du Projet

Le projet est organisé en deux parties :
1. **terraform-aws/** : Infrastructure définie avec Terraform.
2. **opentofu-aws/** : Infrastructure migrée vers OpenTofu.

### Arborescence des fichiers

```
/projet-migration
├── terraform-aws/            # Configuration Terraform
│   ├── main.tf               # Définition des ressources AWS
│   ├── variables.tf          # Variables utilisées par Terraform
│   ├── outputs.tf            # Sorties de l'infrastructure
├── opentofu-aws/             # Configuration OpenTofu (migrée)
│   ├── main.tf               # Définition des ressources AWS
│   ├── variables.tf          # Variables utilisées par OpenTofu
│   ├── outputs.tf            # Sorties de l'infrastructure
├── .gitlab-ci.yml            # Pipeline CI/CD pour GitLab
├── README.md                 # Ce fichier
└── documentation/            # Documentation de la migration
    ├── migration_procedure.md
    └── analysis_report.md
```

## Installation

### Prérequis

- **Terraform** ou **OpenTofu** installé sur votre machine.
- **GitLab CI/CD** configuré sur votre dépôt.
- **TFLint** installé pour la validation de code localement si besoin.

### Installation de OpenTofu

1. Téléchargez la dernière version d'OpenTofu depuis la page [GitHub d'OpenTofu](https://github.com/opentofu/opentofu/releases).
2. Extrayez le fichier dans un répertoire de votre choix (par exemple `C:\opentofu`).
3. Ajoutez ce répertoire à votre variable d'environnement `PATH` pour utiliser la commande `tofu`.

### Commandes de base OpenTofu

- **Initialiser le projet** :
  ```bash
  tofu init
  ```
- **Planifier les changements d'infrastructure** :
  ```bash
  tofu plan
  ```
- **Appliquer les changements** :
  ```bash
  tofu apply -auto-approve
  ```

## Pipeline CI/CD avec GitLab

### Description du Pipeline

Le fichier **`.gitlab-ci.yml`** à la racine du projet définit plusieurs étapes du pipeline CI/CD :

- **Linting (`tflint`)** : Vérifie la qualité du code Terraform ou OpenTofu.
- **Planification (`tofu plan`)** : Génère un plan d'infrastructure détaillant les changements à appliquer.
- **Déploiement manuel (`tofu apply`)** : Applique les changements après validation manuelle.

### Étapes du pipeline

1. **Lint** : Cette étape utilise **TFLint** pour vérifier que votre code suit les bonnes pratiques Terraform/Tofu.
   
2. **Plan** : Cette étape exécute la commande `tofu plan` pour afficher les modifications prévues dans votre infrastructure sans les appliquer.
   
3. **Apply** : Cette étape applique les changements si vous déclenchez manuellement l'exécution dans l'interface GitLab.

### Exécution du pipeline sur GitLab

1. **Commit** et **push** vos modifications sur le dépôt GitLab.
2. Le pipeline sera automatiquement déclenché et exécutera les étapes définies dans **`.gitlab-ci.yml`**.
3. Vous pouvez suivre les résultats de chaque étape directement dans l'interface GitLab CI.

## Documentation de la Migration

La documentation complète du processus de migration de Terraform à OpenTofu est disponible dans le répertoire **documentation/** :

- **migration_procedure.md** : Détaille les étapes de migration, les problèmes rencontrés, et les solutions proposées.
- **analysis_report.md** : Contient une analyse des impacts de la migration sur les projets existants et des recommandations.

## Contribuer

Si vous souhaitez contribuer à ce projet, veuillez suivre ces étapes :

1. Forkez le dépôt.
2. Créez une nouvelle branche (`git checkout -b feature/nom-de-votre-feature`).
3. Committez vos modifications (`git commit -m 'Ajout d'une nouvelle fonctionnalité'`).
4. Pushez vos modifications (`git push origin feature/nom-de-votre-feature`).
5. Ouvrez une Pull Request.

## À propos

Ce projet a été réalisé dans le cadre d'une mission pour explorer la transition entre Terraform et OpenTofu. Il inclut l'automatisation des tests d'infrastructure via GitLab CI.
