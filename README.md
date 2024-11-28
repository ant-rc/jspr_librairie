# jspr_librairie

---

# **1. Présentation**

Le projet consiste à développer un système de gestion simplifié pour une librairie avec deux acteurs principaux :

1. **Gestionnaire** : Responsable de la gestion des livres (ajout et suppression).
2. **Utilisateur** : Capable d'emprunter et de rendre des livres.

## **2. Étapes du Projet**

### **1) Analyse des besoins**

**Cas pratiques** :

- Un gestionnaire ajoute un livre (titre, auteur, année) dans la base.
- Un gestionnaire retire un livre disponible.
- Un utilisateur emprunte un livre disponible.
- Un utilisateur retourne un livre emprunté.

**Questions Clés** :

**Question Livres**

1. Quels attributs essentiels pour chaque livre ?
2. Les livres sont unique ou possède plusieurs copies ? 
3. Comment gérer les livres avec des titres ou auteurs similaires ? Faut-il ajouter un identifiant unique pour chaque livre ?
4. Faut-il intégrer un système de recherche pour trouver des livres (par titre, auteur, année) ?
5. Que faire si un livre est emprunté et qu'il est perdu ou endommagé ?
6. Comment traiter les livres abîmés ou endommagés ? Y a-t-il un mécanisme pour les signaler ou les retirer de la collection ?

**Question d’Emprunt**

1. Que faire si un livre est déjà emprunté ?
2. Que faire si le gestionnaire veut retirer un livre emprunté ?
3. Combien de temps un utilisateur peut-il emprunter un livre ? Faut-il un système de renouvellement ?

**Question Utilisateurs**

1. Comment gérer les livres dont la date de retour est dépassée et qui n'ont pas été rendus ?
2. Faut-il permettre aux utilisateurs de visualiser leur historique d'emprunts passés ?
3. Quels sont les critères pour limiter le nombre de livres qu'un utilisateur peut emprunter ?

### **Scénario (Use Case)**

1. Un gestionnaire ajoute un livre, puis un utilisateur l'emprunte et le rend.
    
    ⇒ le livre est ajouté à la base de données, si déjà existant refuse l’intégration du livre.
    
2. Un utilisateur veut rechercher un livre à emprunter.
    
    ⇒ utilisation d’une barre de recherche par genre, titre, auteur, année…
    
3. Un utilisateur tente d’emprunter un livre déjà emprunté.
    
    ⇒ affichage de la date d’échéance de l’emprunt.
    
4. Un gestionnaire supprime un livre non emprunté.
    
    ⇒ le système refuse la suppression tant que le livre n’est pas rendu.
    
5. L’utilisateur veut consulter son historique d’emprunt.
    
    ⇒ affichage d’un historique d’emprunt (avec date) pour les livres et l’utilisateur.
    

### **2) Structure de données**

Création d’un modèle de données clair avec une base structurée :

- **Livre** :
    - ID : Identifiant unique.
    - Titre : Nom du livre.
    - Auteur : Nom de l’auteur.
    - Année : Année de publication.
    - État : Disponible ou emprunté.
    - Emprunteur : Référence à un utilisateur (null si disponible).
- **Utilisateur** :
    - ID : Identifiant unique.
    - Nom : Nom de l’utilisateur.
    - Rôle : gestionnaire ou utilisateur.
    

Diagramme de données :

- Relation entre "Livre" et "Utilisateur" via une clé étrangère (emprunteur).

| **Entité** | **Attributs** | **Relation** |
| --- | --- | --- |
| **Livre** | ID, Titre, Auteur, Année, État | Un livre peut être emprunté par un utilisateur. |
| **Utilisateur** | ID, Nom, Rôle (gestionnaire/utilisateur) | Un utilisateur peut emprunter plusieurs livres. |
| **Gestionnaire** | ID, Nom, Rôle (gestionnaire) | Un gestionnaire peut ajouter ou supprimer des livres. |

### **3. Use Case**

| **Acteur** | **Cas d'Utilisation** | **Description** |
| --- | --- | --- |
| **Gestionnaire** | Ajouter un livre | Le gestionnaire ajoute un livre dans le système avec des informations comme le titre, l'auteur, l'année, et son état. |
| **Gestionnaire** | Supprimer un livre | Le gestionnaire retire un livre du système, à condition qu'il soit disponible (non emprunté). |
| **Utilisateur** | Emprunter un livre | L'utilisateur choisit un livre disponible et l'emprunte. Il enregistre l’emprunt sous son nom. |
| **Utilisateur** | Rendre un livre | L'utilisateur retourne un livre emprunté, modifiant ainsi son état à "disponible". |

### **4. Implémentation des Tests**

**a). Tests Back-end** 

- **Tests sur les livres** :
    - Création : Vérifier qu’un nouveau livre est ajouté avec des données valides.
    - Lecture : Assurer que la liste des livres est récupérée correctement.
    - Mise à jour : Modifier l’état d’un livre (disponible/emprunté).
    - Suppression : Supprimer un livre disponible uniquement.
- **Tests de validation** :
    - Empêcher l’ajout d’un livre avec des champs vides.
    - Refuser la suppression d’un livre emprunté.

---

**b). Tests Front-end**

- **Interface Gestionnaire** :
    - Afficher correctement la liste des livres.
    - Vérifier que les actions "ajouter" et "supprimer" fonctionnent comme attendu.
- **Interface Utilisateur** :
    - Vérifier que l’emprunt est possible uniquement pour les livres disponibles.
    - Assurer que la liste des livres est mise à jour après un retour.

---
