# propre

Tutoriel : Mise en Place d'un Projet PHP avec GitLab
Dans ce tutoriel, nous allons mettre en place un projet PHP dans GitLab en respectant les exigences spécifiées : tests unitaires, tests d'intégration, analyse de code, maîtrise des commandes Git, configuration des membres et rôles, scripts CI et CD, et développement des classes métiers pour des tests avancés.

1. Configuration de GitLab et Gestion des Comptes
1.1 Invitation des Membres dans GitLab
Connectez-vous à GitLab.
Accédez au projet en cliquant sur le nom du projet.
Dans la barre latérale gauche, sélectionnez "Members".
Cliquez sur "Invite members".
Invitez chaque membre en utilisant leur adresse e-mail.
1.2 Mise en Place des Rôles et Permissions
En tant qu'administrateur, accédez à l'onglet "Members" dans le projet.
Cliquez sur "Edit" à côté du nom de chaque membre.
Sélectionnez le rôle approprié pour chaque membre : Product Owner, Lead-tech, DevOps, etc.
2. Initialisation du Projet dans GitLab
2.1 Création du Dépôt GitLab
Connectez-vous à GitLab.
Cliquez sur l'icône "Plus" dans le coin supérieur droit, puis sélectionnez "New project".
Remplissez les détails du projet : nom, description, visibilité, etc.
Cliquez sur "Create project".
2.2 Configuration de la Branche Principale et des Restrictions d'Accès
Accédez aux "Settings" du projet.
Dans la section "General", modifiez la branche par défaut (par exemple, "main").
Accédez à "Repository" > "Branches" pour configurer les restrictions d'accès à la branche principale.
3. Mise en Place des Pipelines CI/CD
3.1 Configuration du Fichier .gitlab-ci.yml
Créez un fichier .gitlab-ci.yml à la racine du projet.
Ajoutez la configuration du pipeline, y compris les stages, les variables, et les scripts pour chaque étape.
3.2 Exécution des Tests Unitaires
Écrivez des tests unitaires pour vos classes métiers dans le dossier tests.
Modifiez le script de la stage test pour exécuter vos tests unitaires.
3.3 Analyse Statique du Code
Intégrez un outil d'analyse statique du code comme PHPStan ou PHPMD.
Modifiez le script de la stage test pour inclure l'analyse statique du code.
4. Maîtrise des Commandes Git
4.1 Utilisation des Commandes Courantes Git
Expliquez l'utilisation des commandes courantes telles que git add, git commit, git push.
4.2 Gestion des Branches
Détaillez l'utilisation des commandes pour gérer les branches : git branch, git checkout, git merge, git rebase.
5. Configuration Complète du Projet
5.1 Membres, Rôles et Permissions
Vérifiez que chaque membre est correctement configuré avec le rôle approprié et les permissions adéquates.
6. Scripts CI et CD
6.1 Script CI
Expliquez le script CI présent dans .gitlab-ci.yml et comment il exécute les tests, l'analyse statique et d'autres actions nécessaires.
6.2 Script CD
Expliquez le script CD présent et comment il gère le déploiement en tenant compte des différences entre les environnements.
7. Code Correspondant aux Éléments Métiers
7.1 Classes Métiers pour des Tests Avancés
Démontrez les classes métiers et expliquez comment elles permettent l'écriture de tests avancés.




Scripts CI et CD
Script CI (.gitlab-ci.yml)
yaml
Copy code
stages:
  - build
  - test
  - deploy

variables:
  # Définissez ici vos variables d'environnement

before_script:
  - composer install

build:
  stage: build
  script:
    - echo "Build the project"
    # Ajoutez ici les commandes pour construire votre projet

test:
  stage: test
  script:
    - echo "Run unit tests"
    - phpunit
    # Ajoutez ici les commandes pour exécuter vos tests unitaires

  # Ajoutez une section pour les tests d'intégration si nécessaire
  # integration_test:
  #   stage: test
  #   script:
  #     - echo "Run integration tests"
  #     - phpunit --testsuite=integration

deploy:
  stage: deploy
  script:
    - echo "Deploy the project"
    # Ajoutez ici les commandes pour déployer votre projet
Script CD
Le script CD dépendra de la manière dont vous déploierez votre application. Voici un exemple basique pour un déploiement en utilisant SSH et un serveur distant :

bash
Copy code
# Script de déploiement (ex. deploy.sh)

#!/bin/bash

# Déploiement sur un serveur distant via SSH
echo "Deploying the application..."
ssh user@server "cd /path/to/your/app && git pull origin main && composer install && php artisan migrate && php artisan cache:clear"
echo "Deployment completed successfully."
Tests Unitaires et d'Intégration
Voici un exemple simple de tests unitaires et d'intégration pour une classe Reservation en utilisant PHPUnit.

Classe Reservation.php
php
Copy code
<?php

class Reservation {
    private $showId;
    private $seat;
    private $userId;

    public function __construct($showId, $seat, $userId) {
        $this->showId = $showId;
        $this->seat = $seat;
        $this->userId = $userId;
    }

    public function getShowId() {
        return $this->showId;
    }

    public function getSeat() {
        return $this->seat;
    }

    public function getUserId() {
        return $this->userId;
    }
}
Tests Unitaires (ReservationTest.php)
php
Copy code
<?php

use PHPUnit\Framework\TestCase;

class ReservationTest extends TestCase {
    public function testGetShowId() {
        $reservation = new Reservation(1, 'A1', 123);
        $this->assertEquals(1, $reservation->getShowId());
    }

    public function testGetSeat() {
        $reservation = new Reservation(1, 'A1', 123);
        $this->assertEquals('A1', $reservation->getSeat());
    }

    public function testGetUserId() {
        $reservation = new Reservation(1, 'A1', 123);
        $this->assertEquals(123, $reservation->getUserId());
    }
}
Ces exemples sont basiques et peuvent être adaptés en fonction de votre application et de vos besoins spécifiques. Assurez-vous d'ajuster les tests en conséquence pour atteindre une couverture de code d'au moins 70%. Si vous avez des besoins particuliers ou des exigences spécifiques, n'hésitez pas à demander des ajustements ou des ajouts !


CI (Intégration Continue - Continuous Integration) :

L'intégration continue est une pratique de développement logiciel dans laquelle les membres d'une équipe intègrent leur travail fréquemment, généralement plusieurs fois par jour, dans un référentiel partagé. Chaque intégration est ensuite vérifiée par une série automatisée de tests, garantissant ainsi que le nouveau code ne casse pas le fonctionnement de l'application existante. Si un test échoue, l'équipe est alertée, et le code est corrigé rapidement.

Dans le contexte de GitLab et du fichier .gitlab-ci.yml, le test CI est le processus automatisé de compilation, de tests unitaires, d'analyses de code et d'autres vérifications qui sont déclenchés chaque fois qu'un développeur pousse du code dans le référentiel partagé. Ces tests assurent que les nouvelles modifications ne perturbent pas le code existant.

CD (Livraison Continue - Continuous Delivery) :

La livraison continue est une pratique de développement logiciel où chaque modification de code passe par un processus automatisé de build, de tests et de déploiement, permettant ainsi de rendre la nouvelle version du logiciel prête à être déployée en production à tout moment. Contrairement à la mise en production immédiate (Continuous Deployment), dans la livraison continue, le déploiement en production est déclenché manuellement à un moment approprié.

Dans le contexte de GitLab et du fichier .gitlab-ci.yml, le processus CD est défini pour déployer automatiquement l'application ou le service dans un environnement prédéfini (staging, production, etc.) chaque fois que les tests CI réussissent. Le déploiement est souvent conditionné à une validation manuelle ou à d'autres processus organisationnels avant d'atteindre la production.

En résumé, CI garantit que le code est toujours prêt pour une livraison, tandis que CD va plus loin en automatisant le processus de livraison, offrant ainsi la possibilité de déployer rapidement et facilement les modifications dans n'importe quel environnement.
