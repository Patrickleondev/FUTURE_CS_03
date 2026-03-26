# Postman Testing Guide — Task 3 (VAmPI)

Suis ces étapes dans Postman avec ton conteneur Docker VAmPI allumé. 
**Prends des captures d'écran de chaque étape** pour les mettre dans le dossier `evidence` plus tard.

## Étape 1 : Création de compte (Register)
1. **Méthode :** `POST`
2. **URL :** `http://localhost:5000/users/v1/register`
3. **Body (raw > JSON) :**
```json
{
  "username": "intern2026",
  "password": "Password123!",
  "email": "intern@future.test"
}
```
4. **Action :** Clique sur *Send*. 
5. **Preuve :** Capture l'écran montrant le statut `200 OK` et le message de succès.

## Étape 2 : Authentification (Login)
1. **Méthode :** `POST`
2. **URL :** `http://localhost:5000/users/v1/login`
3. **Body (raw > JSON) :**
```json
{
  "username": "intern2026",
  "password": "Password123!"
}
```
4. **Action :** Clique sur *Send*.
5. **Preuve :** Copie la valeur de `auth_token` dans la réponse (c'est ton JWT). Capture l'écran.

## Étape 3 : L'attaque BOLA (Broken Object Level Authorization)
*C'est ici qu'on prouve la faille OWASP API 1.*
1. **Méthode :** `GET`
2. **URL :** `http://localhost:5000/users/v1/admin` *(On demande les infos du compte admin !)*
3. **Onglet "Authorization" :**
   - Type : `Bearer Token`
   - Token : *Colle ici le jeton copié à l'étape 2.*
4. **Action :** Clique sur *Send*.
5. **Résultat attendu :** L'API va te renvoyer les données du compte Admin (email de l'admin, etc.) alors que tu n'es que "intern2026" ! 
6. **Preuve :** Capture cette fuite de données flagrante.

## Étape 4 : Fuite d'informations (Security Misconfiguration)
1. **Méthode :** `GET`
2. **URL :** `http://localhost:5000/users/v1/_debug`
3. **Action :** Clique sur *Send* (sans aucun header, juste comme ça).
4. **Preuve :** Capture l'écran montrant le dump de variables d'environnement, les versions système et la route de débogage laissée active en production.
