# Sensor API

## Description

Sensor API est une API REST développée avec FastAPI qui simule le trafic de clients dans différents magasins. Chaque magasin possède plusieurs capteurs à l’entrée qui permettent de générer le nombre de visiteurs pour une date donnée. L’API prend en compte :

La variabilité normale du trafic par capteur

Les jours de fermeture (ex. dimanche)

Les pannes aléatoires et les pauses de capteurs

La possibilité de consulter les visites par magasin ou par capteur

Ce projet est conçu pour démontrer la gestion de données simulées, la création d’API REST, les tests unitaires et le déploiement sur Render.

## Fonctionnalités principales

Obtenir le trafic total d’un magasin pour une date donnée

Obtenir le trafic d’un capteur spécifique

Simulation de pannes (malfunction) et de pauses (break)

Validation des entrées (date, année, capteur)

Endpoint de healthcheck pour vérifier si l’API fonctionne correctement

## Structure du projet

sensor_api/
│
├─ .github/workflows/ci.yaml       # Configuration CI GitHub Actions
├─ app.py                          # Fichier principal FastAPI
├─ requirements.txt                # Dépendances Python
├─ fake_data_app/
│   ├─ __init__.py                 # Création des magasins et initialisation
│   ├─ sensor.py                   # Classe VisitSensor
│   └─ store.py                    # Classe StoreSensor
└─ tests/
    ├─ test_visit_sensor.py        # Tests unitaires pour VisitSensor
    └─ test_store_methods.py       # Tests unitaires pour StoreSensor

## Installation

### Cloner le projet :

git clone https://github.com/<votre-utilisateur>/sensor_api.git
cd sensor_api

### Créer un environnement virtuel et l’activer :

python3 -m venv .venv
source .venv/bin/activate  # Linux / macOS
.venv\Scripts\activate     # Windows

### Installer les dépendances :

pip install -r requirements.txt
Lancer l’API
uvicorn app:app --reload

### L’API sera accessible à l’adresse : http://127.0.0.1:8000

La documentation interactive Swagger : http://127.0.0.1:8000/docs

## Endpoints

Obtenir le trafic d’un magasin
GET /

Paramètres query :

Paramètre	Type	Description
store_name	str	Nom du magasin (Lille, Paris, Lyon, Toulouse, Marseille)
year	int	Année (>= 2019)
month	int	Mois
day	int	Jour
sensor_id	int, optionnel	ID du capteur (0 à 7)

Exemple :

curl -G https://sensor-api-1-upv8.onrender.com \
     -d "store_name=Lille" \
     -d "year=2023" \
     -d "month=9" \
     -d "day=15"

## Healthcheck

Permet de vérifier que l’API fonctionne correctement

Retourne également la version de Python utilisée

## Tests unitaires

Les tests utilisent le module unittest :

tests/test_visit_sensor.py : tests pour VisitSensor

tests/test_store_methods.py : tests pour StoreSensor

Exécuter tous les tests :

python -m unittest discover tests

## Déploiement

L’API est déployée sur Render : https://sensor-api-1-upv8.onrender.com
