# Jenkins

## Introduction à Jenkins
Jenkins est un outil open-source d'intégration continue (CI) et de livraison continue (CD). Il permet d'automatiser le processus de développement logiciel, notamment la compilation, les tests, et le déploiement d'applications. Jenkins est largement utilisé pour accélérer le développement logiciel et améliorer la qualité des produits en automatisant les étapes fastidieuses du cycle de vie du développement.<br>

### Définition
Jenkins est un serveur d'automatisation qui aide les équipes de développement à réaliser l'intégration et la livraison continues en automatisant des tâches récurrentes, comme la compilation du code source, l'exécution de tests, la génération de rapports, et même le déploiement d'applications sur des environnements de production ou de test.

### Fonctionnalités principales de Jenkins
- Automatisation du processus de build : Jenkins permet d'automatiser le processus de compilation du code source, de génération de rapports, et de création de versions logicielles. Cela élimine les erreurs humaines et assure que les builds sont réalisés de manière cohérente.
- Exécution des tests : Jenkins permet d'exécuter des tests unitaires et d'intégration sur chaque modification du code pour s'assurer que les nouvelles modifications ne cassent pas le système. Il prend en charge divers outils de test comme **JUnit, NUnit, et Selenium**.
- Intégration avec des outils de gestion de version : Jenkins s'intègre parfaitement avec des outils comme **Git, SVN, et Mercurial** pour récupérer le code source à partir de systèmes de contrôle de version.
- Déploiement continu (CD) : En plus de l'intégration continue, Jenkins peut être configuré pour déployer automatiquement l'application dans des environnements de staging ou de production après la réussite des tests.
- Notifications et alertes : Jenkins peut envoyer des notifications par **email, Slack**, ou d'autres services en cas de réussite ou d'échec d'un job (tâche d'intégration ou de déploiement).
- Extensibilité : Jenkins est hautement extensible grâce à un large éventail de plugins qui permettent d'ajouter de nouvelles fonctionnalités (ex. : support de Docker, déploiement dans le cloud, intégration avec d'autres outils CI/CD, etc.).
- Jenkins est utilisé dans plusieurs domaines du développement logiciel, notamment :
1) Intégration Continue (CI) : Automatise le processus de fusion du code dans une branche principale plusieurs fois par jour pour détecter rapidement les erreurs.
2) Livraison Continue (CD) : Automatise le processus de déploiement des applications en production, garantissant ainsi que le code testé est prêt à être mis en production à tout moment.
3) Tests automatisés : Exécute des tests à chaque modification de code pour détecter les régressions ou erreurs potentielles.
4) Automatisation des déploiements sur des infrastructures complexes : Peut gérer les déploiements sur différents environnements (staging, production) en utilisant des outils comme Docker, Kubernetes, ou Ansible.

### Exemple typique de cas pratique
Voici un exemple typique d’utilisation de Jenkins dans un environnement de développement logiciel :

#### Contexte :
Une équipe de développement travaille sur une application web. Les développeurs effectuent des changements réguliers dans le code source, et ils ont besoin de s’assurer que chaque modification est testée et intégrée dans le système sans causer de régressions. <br>

Déploiement d'un pipeline CI/CD avec Jenkins : <br>

1) Récupération du code source :
Jenkins est configuré pour récupérer automatiquement le code depuis un dépôt GitHub ou GitLab chaque fois qu'une modification est poussée (par exemple, un "push" sur la branche develop).
2) Compilation du code :
Après avoir récupéré le code, Jenkins lance un job pour compiler l'application, par exemple en utilisant Maven pour une application Java, ou un script npm pour une application Node.js.
3) Exécution des tests :
Jenkins exécute ensuite une série de tests unitaires et d’intégration. Par exemple, il pourrait utiliser JUnit pour les tests Java ou Mocha pour les tests JavaScript.
4) Rapport de tests :
Jenkins génère un rapport détaillant les résultats des tests. Si un test échoue, Jenkins envoie une notification aux développeurs pour qu'ils corrigent l’erreur.
5) Déploiement automatisé :
Si toutes les étapes précédentes réussissent, Jenkins déploie automatiquement l'application dans un environnement de staging pour validation. Par exemple, il pourrait utiliser Docker pour créer une image et la déployer sur un serveur.
6) Notification :
Enfin, Jenkins envoie des notifications par e-mail ou via Slack pour informer l’équipe du succès ou de l’échec du pipeline CI/CD. Les notifications contiennent généralement des liens vers les rapports de tests ou les logs détaillés.
7) Avantages de Jenkins :
- Automatisation des processus répétitifs : Jenkins permet d'automatiser des tâches répétitives et de réduire l’effort manuel, ce qui améliore la productivité des équipes.
- Détection précoce des erreurs : En exécutant des tests de manière continue, Jenkins permet de détecter rapidement les erreurs et de réduire les risques d’introduire des bugs dans la version finale.
- Réduction du cycle de livraison : Grâce à l'intégration et la livraison continues, Jenkins permet de livrer de nouvelles versions du logiciel plus rapidement et de manière plus fiable.
- Extensibilité avec des plugins : Jenkins offre un vaste écosystème de plugins, ce qui permet de l’adapter à presque tous les processus de développement logiciel et à différentes technologies.

### Conclusion
Jenkins est un outil puissant qui améliore la productivité des équipes de développement en automatisant les processus d'intégration et de déploiement. Il est idéal pour les environnements de développement agile où les modifications fréquentes du code doivent être intégrées, testées et déployées rapidement.

Si tu veux automatiser tes processus de développement, tester et déployer plus efficacement, Jenkins est l'outil à considérer, avec son large éventail de plugins et sa capacité à s'intégrer avec presque tous les outils modernes utilisés dans le développement logiciel.

## Installation

### Configurer la VM:
1) Autoriser l'accès au `localhost:8080` en configurant le pare-feu GCP: Console GCP > Réseau NPC > Pare-feu > Créer une règle de pare-feu
- Nom : "allow-jenkins"
- Cible : Toutes les instances du réseau
- Plage : `0.0.0.0/0`
- Protocoles et ports : cocher TCP en renseignant : `8080`

2) Installer [Jenkins](https://www.jenkins.io/doc/book/installing/linux/) : "Long Term Support release":
```
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

3) Installer [Jenkins](https://www.jenkins.io/doc/book/installing/linux/) : "Installation of Java":
```
sudo apt update
sudo apt install fontconfig openjdk-21-jre
java -version
openjdk version "21.0.3" 2024-04-16
OpenJDK Runtime Environment (build 21.0.3+11-Debian-2)
OpenJDK 64-Bit Server VM (build 21.0.3+11-Debian-2, mixed mode, sharing)
```

4) Installer OpenJDK : `sudo apt install openjdk-17-jdk`

5) Vérifier l'installation :
- Jenkins : `jenkins --version`
- Java : `java -version`

6) Relancer le service Jenkins : `sudo systemctl restart jenkins`

7) Récupérer le mot de passe administrateur : `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`

8) Accéder à la console Jenkins : `http://$IP_VM:8080`

9) Installer les plugins suggérés

10) Créer un compte Jenkins:
- Nom d'utilisateur : `admin`
- Mot de passe : `f3hE3iMw6Aq2B7`
- Nom complet : `admin`
- Adresse email: `admin@example.fr`

## Cas pratique
Lien [Youtube](https://www.youtube.com/watch?v=Gy4Nk2pIuNs&list=PLn6POgpklwWr19VXuoVgIr32HCu0MGNt9&index=3)

### Création de job
1) Accéder à la console Jenkins : `http://$IP_VM:8080`
2) Se connecter avec ses identifiants récupérés précèdemment$
3) `+ Créer un Job` > Job Freestyle (en lui donnant un nom : ici "first_project")
4) Ne modifier aucun paramètre hormis : Ajouter une étape au build > Exécuter un script shell. Puis renseigner : `echo "Hello World!"`
5) Sauvegarder le job
6) Se rendre sur notre job "first_project" et le lancer manuellement en cliquant sur "Lancer un build"
7) Cela génère un premier build indenté "1" sur lequel on peut obtenir des informations:
- Nom du runner
- Date d'exécution
- Sortie de la console
- Changements induits


### Les types de Job
1. **Freestyle** : job générique configurable depuis l'interface graphique afin d'exécuter des tâches simples. Il permet de définir une série d'étapes à exécuter sur ton code source, comme:
- Compilation du code
- Exécution des tests
- Déploiement ou publication
- Envoi de notifications après l'exécution du job
Cas d'usages :
- Déclenchements manuels ou automatiques (ex: commit dans un dépôt Git)
- Intégration d'outils comme Git, maven, Ant, Gradle ou des scripts personnalisés
- Configurable pour utiliser des tests après la compilation afin de déployer les artefacts générés sur un serveur

2. **Pipeline** : job avancé et flexible souvent utilisé dans des processus CI/CD complexes. Un pipeline est défini en tant que code avec un fichier _Jenkinsfile_ contenant la définition du processus d'intégration et de livraison continue sous forme de script (avec **Groovy** pour décrire les étapes)
Cas d'usages :
- Déploiement d'applications sur plusieurs environnements (staging, production)
- Utilisation dans des processus DevOps complexes où tu as des étapes comme _build, test, deploy, etc_, définies dans un fichier versionné (le Jenkinsfile).
- Création de pipelines multibranches où chaque branche du dépôt Git a son propre pipeline

Exemple de Jenkinsfile :
```
# groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'scp target/app.war user@server:/path/to/deploy'
            }
        }
    }
}
```

3. **Multibranch pipeline** : version plus avancée du pipeline permettant de gérer plusieurs branches de ton dépôt Git. Où chaque branche peut avoir son propre pipeline qui est créé automatiquement lorsqu'une nouvelle branche est ajoutée (chaque branche ayant son propre fichier Jenkinsfile associé).
Cas d'usages :
- Travail avec des branches Git multiples et que chaque branche doit avoir son propre pipeline CI/CD (ex: branche _develop_ et _master_ aient des étapes de tests et de déploiement distinctes)

4. **GitHub Organization** : permet de configurer un pipeline qui exécute des actions sur tous les dépôts GitHub d'une organisation. 
Cas d'usages :
- Déclencher des builds sur tous les dépôts d'une organisation GitHub
- Créer une stratégie de CI/CD centralisée pour une organisation entière. 

5. **External Job** : permet la surveillance d'un travail effectué à l'extérieur de Jenkins, comme un job sur un autre serveur ou système. 
Cas d'usages :
- Utilisation de systèmes externes pour certaines tâches (ex: compilation sur un autre serveur OU synchronisation avec un autre système)
- Suivi des travaux non directement gérés par Jenkibs mais devant être intégrés dans un processus plus large

6. **Builds Parallèles** : permet de définir plusieurs configurations ou versions de build à exécuter simultanément.
Cas d'usages : 
- Exécuter des tests sur plusieurs environnements ou configurations (ex: un test pourrait être exécuté sur plusieurs versions de Python ou différents systèmes d'exploitations)

7. **Pipeline as Code** : permet d'inclure la définition du pipeline dans un fichier source versionné, comme un fichier Jenkinsfile dans ton dépôt Git. Ce fichier décrit l'intégralité du pipeline, de l'intégration à la mise en production. 
Cas d'usages : 
- Gestion des pipelines dans un contrôle de version, permettant d'avoir un historique des modifications de pipeline et de le versionner de manière transparente
- Facilite la collaboration entre les équipes de développement et DevOps

8. **Delivery Pipeline** : utilisé pour visualiser et orchestrer un processus de livraison continue. Il permet de suivre plusieurs étapes de déploiement, de tests et de validation dans un processus CI/CD.
Cas d'usages : 
- Suivre visuellement les étapes d'intégration, de tests et de déploiement
- Avoir une vue globale de l'état des différentes versions de ton application dans des environnements comme _staging, production, etc_


### [Users et rôles](https://www.youtube.com/watch?v=wO3weh1fXiQ&list=PLn6POgpklwWr19VXuoVgIr32HCu0MGNt9&index=5)
_Pré-requis_ :
- Créer deux nouveaux utilisateurs : `player1` & `player2` (mdp: pwd1/pwd2 ; email:player1/player2@example.fr)
- Créer deux nouveaux builds : `PythonBuildTest` & `JavaBuildTest` afin de tester le système de groupe (build : `echo "Ceci est un build Python(/Java)`)

Utilisation du plugin "**Role-based Authorization Strategy**" afin de gérer les _rôles_ (groupes d'ensemble de users) et les _users_ eux-mêmes afin d'affecter des status (ex: développeurs, admin, etc) et des patterns de jobs à un rôle (ex: Java, Python).
- Aller dans l'onglet "Administrer Jenkins" > "Security" et sélectionner "Stratégie basée sur les rôles" dans la liste déroulante de la section _Autorisations_ afin d'activer le plugin installé.
- Pour ensuite créer des rôles et les gérer, se rendre dans l'onglet "Administrer Jenkins" > "Gérer les rôles". 

