Hello
🔥 TP : Intégration Continue avec Jenkins et Docker pour une Application Python 🔥
🎯 Objectif
Mettre en place un pipeline CI/CD avec Jenkins et Docker pour automatiser le build, les tests et le déploiement d'une application Python.

📋 Pré-requis
Docker installé ✅
Jenkins installé en local ✅
Python installé ✅
Git installé ✅
📌 Étape 1 : Préparer l'application Python
Nous allons créer une petite application Python avec Flask et un test unitaire.

📝 Structure du projet
bash
Copier
Modifie
``````
/docker-python-app
│── app.py
│── requirements.txt
│── Dockerfile
│── test_app.py
│── jenkinsfile
│── .gitignore
└── README.md
```
📌 Étape 2 : Créer l'application Flask
Dans app.py, ajoute le code suivant :

python
Copier
Modifier
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, Docker & Jenkins!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
📌 Étape 3 : Ajouter les dépendances
Dans requirements.txt, ajoute :

nginx
Copier
Modifier
flask
pytest
requests
📌 Étape 4 : Ajouter un test unitaire
Dans test_app.py, ajoute :

python
Copier
Modifier
import pytest
from app import app

@pytest.fixture
def client():
    app.testing = True
    return app.test_client()

def test_home(client):
    response = client.get('/')
    assert response.status_code == 200
    assert b"Hello, Docker & Jenkins!" in response.data
📌 Étape 5 : Créer un Dockerfile
Ce fichier permettra de dockeriser l’application.

Dockerfile
Copier
Modifier
# Utiliser l'image Python officielle
FROM python:3.9

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers de l'application
COPY . .

# Installer les dépendances
RUN pip install --no-cache-dir -r requirements.txt

# Exposer le port 5000
EXPOSE 5000

# Démarrer l'application
CMD ["python", "app.py"]
📌 Étape 6 : Créer un Jenkinsfile
Le Jenkinsfile définit le pipeline CI/CD.

groovy
Copier
Modifier
pipeline {
    agent {
        docker {
            image 'python:3.9'
        }
    }
    
    environment {
        APP_NAME = "docker-python-app"
    }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ton-repo/docker-python-app.git'
            }
        }
        
        stage('Install dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        
        stage('Run tests') {
            steps {
                sh 'pytest test_app.py'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $APP_NAME .'
            }
        }
        
        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 5000:5000 $APP_NAME'
            }
        }
    }
}
📌 Étape 7 : Lancer le pipeline dans Jenkins
🚀 Démarrer Jenkins et configurer le projet
Accède à Jenkins : http://localhost:8080
Crée un nouveau projet Pipeline.
Choisis Pipeline script from SCM et renseigne l’URL du dépôt Git.
Sauvegarde et lance le build.
📌 Étape 8 : Vérifier le déploiement
Après l’exécution du pipeline :

Vérifie si le conteneur tourne :
sh
Copier
Modifier
docker ps
Teste l’application dans un navigateur :
arduino
Copier
Modifier
http://localhost:5000
✅ Félicitations ! 🎉
Tu as maintenant un pipeline CI/CD complet avec Jenkins, Docker et une application Python Flask !

🔥 Améliorations possibles :

Ajouter un service PostgreSQL ou Redis avec docker-compose
Déployer sur AWS, GCP ou Azure
Automatiser les tests avec GitHub Actions en plus de Jenkins
🚀 Prêt à tester ce TP ? 😊