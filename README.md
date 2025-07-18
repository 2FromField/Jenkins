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

