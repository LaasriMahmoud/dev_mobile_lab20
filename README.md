# 📞 Lab 20 : Application Number Book avec Android, Contacts et API distante via Retrofit

## 📋 Présentation du Projet
Ce laboratoire complet démontre comment interconnecter une application Android native avec un serveur backend distant et une base de données MySQL. 
L'application **NumberBook** permet de lire les contacts locaux du téléphone, de les afficher, puis de les synchroniser vers un serveur Web PHP/MySQL. Elle propose également une fonctionnalité de recherche en temps réel sur la base distante.

---

## 🎯 Objectifs Pédagogiques
- Lire et manipuler les données système Android à l'aide de `ContentResolver` et `Cursor`.
- Gérer dynamiquement les **Permissions** à l'exécution (`READ_CONTACTS`).
- Configurer et utiliser la bibliothèque **Retrofit** pour effectuer des requêtes réseau HTTP (POST/GET).
- Sérialiser et désérialiser des objets Java au format JSON en utilisant la bibliothèque **Gson**.
- Développer un **Backend PHP** structuré avec une architecture propre et sécurisée (classes Database, Model, Service, API).
- Concevoir un schéma de base de données relationnel optimal avec MySQL.

---

## 🏗️ Architecture Globale du Projet

Le projet comporte deux parties principales :

### 1. Backend PHP / MySQL (`numberbook-api/`)
- `config/Database.php` : Connexion à la base avec PDO (utilisation de l'encodage `utf8mb4`).
- `model/Contact.php` : Classe de représentation logique de l'objet Contact.
- `service/ContactService.php` : Contient la logique d'accès aux données (requêtes préparées SQL pour contrer les injections SQL).
- `api/insertContact.php` : Reçoit une requête HTTP POST contenant un JSON pour insérer un contact.
- `api/getAllContacts.php` : Renvoie la liste complète des contacts encodée en JSON.
- `api/searchContact.php` : Effectue une recherche SQL `LIKE` partielle par mot-clé et renvoie les résultats en JSON.
- `database.sql` : Script SQL de création de la base de données `numberbook` et de sa table `contact`.

### 2. Client Android Java
- `Contact.java` & `ApiResponse.java` : Modèles de données désérialisés automatiquement par GSON.
- `ContactApi.java` : Interface déclarant les routes HTTP via les annotations Retrofit (`@POST`, `@GET`, `@Query`).
- `RetrofitClient.java` : Classe Singleton fournissant l'instance globale de configuration réseau Retrofit.
- `ContactAdapter.java` : Adaptateur RecyclerView utilisant le layout standard `simple_list_item_2` pour afficher les contacts.
- `MainActivity.java` : Cœur de l'application gérant les permissions Android, l'affichage et les boutons d'actions.

---

## 🧪 Guide des Tests et Validation
1. **Initialisation** : Importez le script `database.sql` dans votre gestionnaire MySQL local.
2. **Déploiement Backend** : Déposez le dossier `numberbook-api` dans votre répertoire de serveur Web (WAMP/XAMPP).
3. **Configuration IP** : Dans `RetrofitClient.java`, remplacez l'IP `192.168.1.10` par l'adresse IP locale de votre machine exécutant le serveur.
4. **Permissions** : Au clic sur "Charger les contacts", refusez puis acceptez la permission pour tester le comportement réactif.
5. **Synchronisation** : Chargez les contacts locaux puis cliquez sur "Synchroniser vers le serveur" pour insérer les contacts dans la base de données distante.
6. **Recherche Distante** : Saisissez un mot-clé (Nom ou Numéro) dans le champ de texte et cliquez sur "Rechercher" pour interroger la base SQL distante.