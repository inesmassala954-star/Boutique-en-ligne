# Boutique en ligne

Ce projet est une petite boutique de démonstration réalisée en HTML, CSS et JavaScript natif. Elle affiche un catalogue de produits, permet de composer un panier et conserve son contenu dans le stockage local du navigateur.

## Fonctionnalités

- Affichage des produits du catalogue avec leur nom, leur description, leur image et leur prix en euros.
- Recherche des produits par nom.
- Saisie et contrôle d'une quantité, puis ajout au panier.
- Retrait d'un produit du panier et mise à jour automatique du total.
- Restauration du panier après rechargement de la page grâce à `localStorage`.
- Deux catalogues d'exemple : des peluches et des chaises.

## Lancer le projet

Aucune installation ni compilation n'est nécessaire : le projet utilise les fonctionnalités natives du navigateur.

1. Ouvrir `mini-projet-js-2026.html` dans un navigateur.
2. Si le navigateur restreint certaines fonctionnalités en ouvrant directement le fichier, servir le dossier avec un serveur HTTP local statique, puis ouvrir la page à l'adresse indiquée par ce serveur.

Le fichier HTML charge les styles, le catalogue sélectionné et le script de la boutique. Il n'y a pas de serveur applicatif ni de procédure de déploiement configurés dans le dépôt.

## Utiliser un autre catalogue

Par défaut, `mini-projet-js-2026.html` charge `data/catalog1.js` :

```html
<script src="./data/catalog1.js"></script>
<!-- <script src="data/catalog2.js"></script> -->
```

Pour afficher les chaises, commenter la première ligne de script et décommenter la seconde. Il faut charger un seul catalogue à la fois, car chacun déclare la variable globale `catalog`.

## Organisation des fichiers

```text
mini-projet-js-2026.html  Page principale et choix du catalogue
data/
  catalog1.js            Catalogue de peluches
  catalog2.js            Catalogue de chaises
images/                  Images utilisées par les catalogues
scripts/
  projet2026.js           Affichage, recherche et gestion du panier
style/
  style-projet2026.css    Mise en page générale
  boutique.css           Styles des produits, contrôles et panier
```

Les chemins d'images sont définis relativement au dossier du projet, par exemple `images/nounours1.jpg`.

## Format d'un produit

Chaque fichier de catalogue définit un tableau global nommé `catalog`. Un produit contient les propriétés suivantes :

```js
{
  name: "Nounours marron",
  description: "Un joli nounours marron avec un foulard",
  image: "images/nounours1.jpg",
  price: 35
}
```

Pour ajouter un produit, ajouter un objet au tableau et vérifier que le chemin de son image existe. La propriété `qty` présente dans le premier catalogue n'est pas utilisée pour limiter les commandes dans le script actuel.

## Fonctionnement du panier

Le script `scripts/projet2026.js` crée les éléments de la boutique à partir de `catalog`, gère les contrôles de quantité, les ajouts et les retraits, puis recalcule le total. La recherche masque les produits dont le nom ne contient pas le texte saisi.

Le panier est enregistré dans `localStorage` sous la clé `cart`. Il est donc propre au navigateur et au profil utilisés ; il n'est pas partagé entre appareils et peut être effacé en supprimant les données du site dans le navigateur.

## Limites actuelles

- Il s'agit d'une démonstration côté navigateur : aucun compte, paiement, envoi de commande ou stockage serveur n'est implémenté.
- Les quantités en stock des catalogues ne sont pas consultées.
- La quantité saisie pour une commande est ramenée à zéro à partir de `MAX_QTY` (9), tandis que la quantité cumulée d'une ligne de panier est plafonnée à 9.
- Aucun script de tests, linter ou outil de build n'est fourni.