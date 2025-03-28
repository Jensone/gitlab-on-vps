Pour configurer une tâche (ou "job") à exécuter sur votre GitLab Runner, vous devez créer un pipeline CI/CD en définissant les étapes et les tâches correspondantes dans un fichier `.gitlab-ci.yml` placé à la racine de votre projet. Voici comment procéder :

**Étape 1 : Création du fichier `.gitlab-ci.yml`**

Ce fichier est essentiel pour orchestrer les différentes tâches de votre pipeline. Il décrit les étapes (stages) et les tâches (jobs) à exécuter. Chaque tâche peut inclure des scripts spécifiques, des variables, des artefacts, etc.

Voici un exemple simple de fichier `.gitlab-ci.yml` :


```yaml
stages:
  - build
  - test
  - deploy

build-job:
  stage: build
  script:
    - echo "Compilation de l'application..."
    - # Commandes pour compiler votre application

test-job:
  stage: test
  script:
    - echo "Exécution des tests..."
    - # Commandes pour exécuter les tests

deploy-job:
  stage: deploy
  script:
    - echo "Déploiement de l'application..."
    - # Commandes pour déployer votre application
```


Dans cet exemple :

- **stages** : Définit les différentes étapes du pipeline.
- **build-job** : Tâche associée à l'étape de compilation.
- **test-job** : Tâche associée à l'étape de test.
- **deploy-job** : Tâche associée à l'étape de déploiement.

**Étape 2 : Personnalisation des tâches**

Vous pouvez personnaliser chaque tâche en fonction de vos besoins spécifiques. Par exemple, pour utiliser une image Docker spécifique ou définir des variables d'environnement :


```yaml
build-job:
  stage: build
  image: node:14
  script:
    - echo "Installation des dépendances..."
    - npm install
    - echo "Compilation de l'application..."
    - npm run build
```


Dans cet exemple, l'image Docker Node.js 14 est utilisée pour exécuter les commandes de construction de l'application.

**Étape 3 : Utilisation des tags pour cibler un Runner spécifique**

Si vous avez configuré des tags lors de l'enregistrement de votre GitLab Runner, vous pouvez les utiliser pour diriger certaines tâches vers des Runners spécifiques :


```yaml
test-job:
  stage: test
  tags:
    - mon-runner-tag
  script:
    - echo "Exécution des tests sur le Runner spécifié..."
    - # Commandes pour exécuter les tests
```


Assurez-vous que le Runner enregistré possède le tag correspondant pour qu'il prenne en charge cette tâche.

**Étape 4 : Validation et exécution du pipeline**

Après avoir défini votre fichier `.gitlab-ci.yml`, poussez-le dans votre dépôt GitLab. GitLab détectera automatiquement ce fichier et déclenchera le pipeline défini à chaque nouvelle modification apportée au dépôt. Vous pouvez suivre l'exécution du pipeline et l'état de chaque tâche via l'interface GitLab, sous l'onglet **CI/CD > Pipelines**.
