# Task 3 Strategy & Experimentation Guide — API Security (VAmPI)

**Target API Selected:** VAmPI (Vulnerable API made with Flask)  
**Goal:** Manually experiment with the API using Postman to generate screenshot evidence for the `images/` directory.

---

## 🏗️ 1. Environment & Setup

VAmPI must be hosted locally to avoid unauthorized exploitation of external systems.

1. **Démarrer le conteneur Docker :**
   ```bash
   docker run -p 5000:5000 erev0s/vampi
   ```
2. **Initialiser la base de données (ABSOLUMENT REQUIS) :**
   Dans ton navigateur ou via Postman, fais une simple requête `GET` sur :
   `http://127.0.0.1:5000/createdb`
   *(Si tu ne fais pas ça, tu auras des erreurs de base de données partout !)*

3. **Explorer Swagger UI (Optionnel) :**
   Visite `http://127.0.0.1:5000/ui/` pour voir toute la documentation interactive.

---

## 🗺️ 2. Liste Complète des Endpoints (API Map)

Voici toutes les actions possibles sur l'API VAmPI. Utilise Postman pour les tester une à une et comprendre le flux (Flow).

| Action | Path | Details |
|---|---|---|
| **GET** | `/createdb` | Crée et peuple la base de données avec des fausses données. |
| **GET** | `/` | Page d'accueil de VAmPI. |
| **GET** | `/me` | Affiche l'utilisateur actuellement connecté (via le Token). |
| **GET** | `/users/v1` | Affiche tous les utilisateurs avec des infos basiques (Enumération). |
| **GET** | `/users/v1/_debug` | Affiche TOUS les détails de TOUS les utilisateurs (Faille BFLA). |
| **POST** | `/users/v1/register` | Créer un nouvel utilisateur. |
| **POST** | `/users/v1/login` | Connexion -> Récupération du JWT. |
| **GET** | `/users/v1/{username}` | Affiche un utilisateur spécifique (Faille BOLA). |
| **DELETE**| `/users/v1/{username}` | Supprime un utilisateur (Censé être réservé aux Admins). |
| **PUT** | `/users/v1/{username}/email`| Met à jour l'email d'un utilisateur. |
| **PUT** | `/users/v1/{username}/password`| Met à jour le mot de passe (Faille de contournement possible). |
| **GET** | `/books/v1` | Récupère la liste de tous les livres. |
| **POST** | `/books/v1` | Ajoute un nouveau livre (titre + secret). |
| **GET** | `/books/v1/{book}` | Récupère le livre et son secret par titre. |

---

## 🧪 3. Scénarios d'Exploitation (À tester dans Postman)

Pour générer tes captures d'écran et prouver les failles, réalise ces 3 attaques principales :

### Attaque A : Broken Object Level Authorization (BOLA)
1. Créée ton compte : `POST http://localhost:5000/users/v1/register` avec le body `{"username": "intern", "password": "123", "email": "a@b.c"}`
2. Connecte-toi : `POST http://localhost:5000/users/v1/login`. **Copie le JWT (auth_token)**.
3. Vole les données admin : Envoie `GET http://localhost:5000/users/v1/admin`. Dans Postman, va dans l'onglet *Authorization*, choisis *Bearer Token*, et colle ton JWT.
   👉 **Capture d'écran 1 :** La réponse de l'API dévoilant les données de l'admin alors que tu es "intern". Sauvegarde dans `images/bola_exploit.png`.

### Attaque B : Excessive Data Exposure & BFLA (Debug Endpoint)
Cette route est censée être réservée aux développeurs en interne.
1. Envoie une requête `GET http://localhost:5000/users/v1/_debug` (Sans aucune authentification).
2. Observe que la base de données entière "fuit" (mots de passe chiffrés, tous les comptes).
   👉 **Capture d'écran 2 :** La fuite massive d'informations. Sauvegarde dans `images/debug_exposure.png`.

### Attaque C : API Information Enumeration
Même sans être connecté, l'API fournit trop d'informations publiques.
1. Envoie `GET http://localhost:5000/users/v1`.
2. Observe que tu peux lister l'intégralité des noms d'utilisateurs inscrits.
   👉 **Capture d'écran 3 :** La liste des utilisateurs prouvant le User Enumeration. Sauvegarde dans `images/user_enumeration.png`.

---

## 📤 4. Finalisation
Une fois que tu as expérimenté sur ces routes avec Postman et placé tes captures d'écran dans le dossier `images/`, tu auras tout le matériel pratique pour étayer le rapport théorique `API_Security_Risk_Analysis_Report.md`. 

*Note : Le script `vampi_exploit.py` automatise les attaques A et B pour prouver que les hackers scripteraient ces vulnérabilités à grande échelle.*
