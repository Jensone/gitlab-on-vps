L'installation de GitLab et de GitLab Runner sur un VPS Ubuntu vous permettra de gérer votre propre plateforme DevOps et d'automatiser vos processus CI/CD. Voici un guide détaillé pour accomplir cette tâche.

**Prérequis :**

- Un VPS fonctionnant sous Ubuntu.
- Accès avec des privilèges sudo.
- Une connexion Internet stable.

**Étape 1 : Mise à jour des paquets Ubuntu**

Avant de commencer, assurez-vous que votre système est à jour :


```bash
sudo apt update && sudo apt upgrade -y
```


**Étape 2 : Installation de GitLab**

1. **Installer les dépendances requises :**

   ```bash
   sudo apt install -y curl openssh-server ca-certificates
   ```


2. **Ajouter le dépôt GitLab :**

   ```bash
   curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
   ```


3. **Installer GitLab Community Edition :**

   Remplacez `votre_domaine` par le nom de domaine ou l'adresse IP de votre serveur.

   ```bash
   sudo EXTERNAL_URL="http://votre_domaine" apt install gitlab-ce
   ```


4. **Configurer GitLab :**

   Après l'installation, GitLab s'initialisera automatiquement. Accédez à `http://votre_domaine` dans votre navigateur pour finaliser la configuration initiale et définir le mot de passe administrateur.

**Étape 3 : Installation de GitLab Runner**

1. **Ajouter le dépôt officiel de GitLab Runner :**

   ```bash
   curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh | sudo bash
   ```

2. **Installer GitLab Runner :**

   ```bash
   sudo apt install gitlab-runner
   ```

**Étape 4 : Enregistrement de GitLab Runner**

1. **Obtenir le jeton d'enregistrement :**

   Dans l'interface GitLab, accédez à votre projet, puis à **Paramètres > CI/CD > Runners**. Copiez le jeton d'enregistrement disponible.

2. **Enregistrer le Runner :**

   Exécutez la commande suivante et suivez les invites :

   ```bash
   sudo gitlab-runner register
   ```

   Lors de l'enregistrement :

   - **URL de GitLab CI :** Entrez l'URL de votre instance GitLab, par exemple `http://votre_domaine`.
   - **Jeton d'enregistrement :** Collez le jeton copié précédemment.
   - **Description du Runner :** Fournissez une description, par exemple `runner-vps-ubuntu`.
   - **Tags :** Ajoutez des tags pertinents pour identifier le Runner.
   - **Exécuteur :** Choisissez `shell` pour une exécution directe des commandes.

**Étape 5 : Démarrage et activation du service GitLab Runner**

1. **Démarrer le service :**

   ```bash
   sudo gitlab-runner start
   ```


2. **Activer le démarrage automatique :**

   ```bash
   sudo systemctl enable gitlab-runner
   ```


**Étape 6 : Vérification du statut du Runner**

Pour confirmer que le Runner est opérationnel et enregistré auprès de votre instance GitLab :


```bash
sudo gitlab-runner verify
```

Vous devriez voir une confirmation indiquant que le Runner est valide et prêt à accepter des tâches.
