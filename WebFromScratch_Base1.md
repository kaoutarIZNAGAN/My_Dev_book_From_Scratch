# Culture générale :

## comprendre le focntionnement du codage:

- les unités de Js :
  comme nous les humains sommes capables de lire le langage naturelle, la machine qui execute le code est capable de lire un langage de programmation via un standard predefinis dans la conception du langage. comme on le siat la machine traite uniquement des signaux binaires 0 ou 1, equivalents à tension basse et tension haute dans les circuits physiques de la machine. donc pour que js puisse etre executé sur la machine, il faut qu'elle transforme le langage naturelle en instructions en 0 et 1. voici comment ça se passe :

1️⃣ VS Code (éditeur):

```js
let a = 1;
let b = 2;
let c = a + b; // 3
```

VS Code sauvegarde un fichier .js

Le fichier est stocké en UTF-8

Donc physiquement : une suite de bytes

Exemple simplifié :

6C 65 74 20 61 20 3D 20 31 ...

Ce sont déjà des 0 et 1 stockés sur ton SSD.

2️⃣ Stockage SSD

Le SSD garde ces bits dans des cellules flash :

électrons piégés → 0

pas d’électrons → 1

Ton fichier devient un état électrique figé.

3️⃣ Tu exécutes le fichier (Node ou navigateur)

L’OS intervient :

Il charge Node.js ou Chrome en mémoire (RAM)

Il charge ton fichier .js en RAM

Il donne un espace mémoire au processus

🧠 4️⃣ Le moteur JS (V8)

V8 fait 3 choses :

1. Parsing

Il lit ton texte et vérifie la syntaxe.

2. AST (arbre syntaxique)

Ton code devient :

VariableDeclaration
├── a = 1
├── b = 2
└── c = a + b

Ce n’est plus du texte.
C’est une structure interne en mémoire.

3. Compilation JIT

V8 transforme ça en instructions machine adaptées à ton CPU.

⚙️ 5️⃣ Code machine

Ton addition devient quelque chose comme :

MOV R1, 1
MOV R2, 2
ADD R1, R2
MOV R3, R1

Chaque instruction = une suite de bits.

Exemple fictif :

10101010 00000001
11000011 00000010
🧮 6️⃣ CPU entre en jeu

Le CPU fonctionne en cycle :

Fetch (chercher instruction en RAM)

Decode

Execute

Il lit l’instruction ADD.

🔢 7️⃣ ALU fait l’addition

En binaire :

1 = 0001
2 = 0010

---

3 = 0011

L’ALU contient :

des portes XOR

des portes AND

des portes OR

Ces portes sont faites de transistors.

⚡ 8️⃣ Niveau transistor

Un transistor est un interrupteur :

tension haute → courant passe → 1

tension basse → bloqué → 0

Pendant l’addition :

des milliards de transistors changent d’état

en quelques nanosecondes

synchronisés par l’horloge CPU

C’est littéralement des électrons qui bougent dans du silicium.

💾 9️⃣ Résultat stocké

Le résultat 3 :

est placé dans un registre CPU

puis peut être écrit en RAM

puis utilisé par le moteur JS

🔁 1️⃣0️⃣ Retour vers JavaScript

V8 récupère le résultat.

Il associe :

c → valeur interne 3

Dans sa mémoire interne.

🖥 1️⃣1️⃣ Si tu fais console.log(c)

Alors :

V8 convertit le nombre 3 en chaîne "3"

L’OS envoie les données à la console

La console dessine le caractère 3

🎨 1️⃣2️⃣ Affichage écran

Pour afficher "3" :

Le GPU reçoit l’instruction de dessiner un caractère

Le caractère correspond à une police (font)

Le GPU colore des pixels

L’écran active des sous-pixels rouges/verts/bleus

Encore des transistors.
Encore des différences de tension.

Et tu vois :

3

# Langage JS :

### Les catégories en JS

#### Valeurs

```js
42
"hello"
true
[]
{}
```

#### Variables :

```js
let x = 10;
const y = 20;
```

#### Fonctions :

```js
function add(a, b) {}
const add = (a, b) => a + b;
```

#### Méthodes :

Fonctions attachées à un objet

```js
[1, 2, 3].map(...)
"hello".toUpperCase()

📌 Elles s’appellent sur quelque chose
```

#### Instructions (statements):

Contrôlent le flux du programme

```js
if
for
while
switch
return
```

#### Opérateurs :

Produisent une valeur à partir d’expressions

```js
+   -   *
&&  ||  !
=== > <

Et donc 👇

condition ? a : b
```

### Functions:

#### prérequis :

##### Objets:

##### Méthodes:

##### Propriétés :

##### constructeur :

##### héritage :

##### classe :

##### prototype :

à quoi sert le prototype :
✔️ Héritage
✔️ Partage de méthodes
✔️ Performance mémoire
✔️ Base de la POO JS
✔️ Base des class

Le prototype sert principalement à créer une fonction avec "New" et gérer l'héritage.

##### Partamètres :

##### Arguments :

#### Fonction fléchée (arrow function):

##### syntaxe :

- avec un retour explicite : F (item) => {} : un bloc d'instructions, auquel il faudrait ecrire l'instruction retourne si on y souhaite retourner qlq chose.

- avec un retour implicite : F (item) => : sans acolades mais on peut y mettre qu'une seule instruction. le resultat est retourné automatiquement.

##### caractéristiques :

- le "This" dans le cas d'une fonction fléchées n'est pas dynamique, cela veut dire que sa velur est déteminée au moment de la création de la fonction et pas au moment de son appel. il faudrait éviter de l'utiliser dans le cas d'une fonction fléchée.

- une fonction fléchée n'a pas de prototype: elle est crée pour etre utilisée comme une action et non en tant qu'objet.
  une fonction fléchée ne peut pas etre utilisée comme un constructeur, exemple :

```js
const f = () => {};
f.prototype; // undefined

new f(); // ❌ TypeError
```

le code anticipe et evite de créer des objets unitules.

- une fonction fléchée ne peut pas avoir des argments: étant qu'elle n'a pas un contexte d'appel, elle ne peut pas béneficier d'une dynamique, elle ne peut ni avoir des arguments ni utiliser "this" de son propre contexte dynamique.

- le "this" d'une fonction fléchée hérite du this parent.

```js
const user = {
  nom: "Kaoutar",
  direNom() {
    setTimeout(() => {
      console.log(this.nom);
    }, 1000);
  },
};

user.direNom(); // Kaoutar
```

#### Règles et uses cases :

1. quand utiliser une fonction fléchée :
   Utiliser une fonction fléchée quand il faudrait HÉRITER du contexte (this)

- Cas n1: Callback (pas besoin de this, code court et lisibilité maximale)
  ```js
  setTimeout(() => {
    console.log("Hello");
  }, 1000);
  ```
- cas N2: Quand on veut garder le This du parent. exemple dans ce cas le this = instantce de user. dans ce cas, si on remplace la fonction fléchée par une fonction classique, le contxte de this va etre perdu.

  ```js
  function User(nom) {
    this.nom = nom;

    setTimeout(() => {
      console.log(this.nom);
    }, 1000);
  }
  ```

new User("Kaoutar");

````

- Cas n3: pur logique, pur calcul: pas d'objet, pas besoin de this ni de prototype.
  ```js
  const addition = (a, b) => a + b;
````

- Cas n4: ne pas utiliser une fonction fléchée pour créer une méthode d'objet, car une méthde a besoin d'un contexte dynamique.

```js
const user = {
  nom: "Kaoutar",
  afficher: () => {
    console.log(this.nom);
  },
};

user.afficher(); // ❌ undefined
```

2. Quand utiliser une fonction classique:
   Utiliser une fonction classique quand il faudrait CRÉER un contexte (this)

- cas n1: quand on veut créer une méthode d'objet. quand le this doit dépendre de l'objet appelant et que le comportement dynamique est voulu.

```js
const user = {
  nom: "Kaoutar",
  afficher() {
    console.log(this.nom);
  },
};

user.afficher(); // Kaoutar
```

- Cas n2: quand il faut instancier l'objet = créer un constructeur.

```js
function User(nom) {
  this.nom = nom;
}

const u1 = new User("Kaoutar");
```

- Cas n3: quand on souhaite créer un prototype pour optimiser la mémoire et créer des méthodes communes. Programmation orientée Prototype.

function User(nom) {
this.nom = nom;
}

User.prototype.afficher = function () {
console.log(this.nom);
};

#### Conclusion :

- Je construis ou modélise quelque chose : Fonction classique.

- j'execute une action : Fonction fléchée.

pour choisir laquelle, il suffit de répondre à la question :
Est-ce que cette fonction DOIT dépendre de qui l’appelle ?

✅ oui → function  
❌ non → =>

à Retenir :  
✔️ Arrow = logique, callbacks, héritage de this
✔️ Function = méthodes, objets, instances, prototypes, API
✔️ Arrow = jamais méthode
✔️ Function = structure

### Async / await :

#### prérequis :

##### Thread :

##### code synchrone :

##### code asynchrone :

Le code asynchrone permet à JavaScript de ne pas bloquer pendant les opérations lentes.

#### Règles & Use cases :

1. Tout ce qui peut bloquer le serveur ne doit PAS être synchrone (Accès base de données, Requêtes HTTP, Lecture / écriture de fichiers utilisateurs, Appels API externes, Calculs lourds, Authentification lente...). Cela évite les latences et crashs sans bloquer les autres utilisateurs de se servir.

2. Le code synhrone est utilisé en backend dans des cas très spécifiques, exp :

- Au démarrage du serveur (BOOTSTRAP: Charger la configuration -> Vérifier des variables d’environnement -> Lire un petit fichier de config..) executé une seule fois, aucun utilisateur n'est conecté.
- Scripts hors serveur (CLI, jobs, migrations)_Here_
- Opérations très rapides et garanties (calculs simples, manipulation d’objets, validation de données, parsing JSON...)_Here_

### Promises :

### Callbacks:

Prérequis :

#### boucle d'avenement:

#### pile d'appel:

La fonction de rappel s'execute une fois la requete terminée et les resultats reçus. ce qui contirbue à rendre le code non bloquant, d'autres élements entre en jeu, comme la boucle d'evenement et la pile d'appel.

### Arrays methods :

#### Les méthodes :

##### Reduce :

C'est une méthode qui permet de transformer un tableau en une valeur quelque soit son type (Int; Bool; Tab; Objet...), le type de la valeur depend principalement de l'initialisation.

###### Syntaxe :

```js
let result = Tableau.reduce((CallBack(valeur à retourner, valeur cournate du tableau)),Valeur initiale de la valeur à retourner);

```

###### utilisation :

- additionne run tableau
- envoyer un objet de compatge
- fusionner des items d'un objet
- pour faire le role de filter et map mais de preference utiliser chaque méthode pour son besoin pour un maximium de lisibilité.

En général, c'est prendre une collection pour la transformer en une valeur et non simplement l'additionner.

##### Filter() :

##### Map():

### string Méthodes :

#### Split ():

###### Syntaxe :

```js
const str = "The quick brown fox jumps over the lazy dog.";

const words = str.split(" ");
console.log(words[3]);
// Expected output: "fox"

const chars = str.split("");
console.log(chars[8]);
// Expected output: "k"

const strCopy = str.split();
console.log(strCopy);
// Expected output: Array ["The quick brown fox jumps over the lazy dog."]
```

Attention : Ce n'est pas une façon robuste d'inverser une chaîne, Cela ne fonctionne pas si la chaîne de caractères contient des groupes de graphèmes, même en utilisant une division sensible aux unicodes.
exemple :

```js
const str = "résumé";
const strReverse = str.split(/(?:)/u).reverse().join("");
// => "́emuśer"
```

# Git

## Architetcure GIT :

### Prérequis :

- Repo : dossier
- commit : image du code dans un instant t. c'est ce qui permet de retourner à une ancienne version, car elle est sauvegardé sous un commit précis et versionné.

### le Wrkflow commandes git :

comprendre ce qui se passe entre le add . et commit et push.

le code vit sur 4 endroits quand on utilise git comme moyen de versioning et d'archivage:

- local working direction (dossier et path sur le pc), via la commande git clone, un projet peut etre recupéré du repo distant et sauvegardé dans le repo local. puis grace au git checkout le dossier est sauvegardé dans le local work direction.
- staging area (un endroit de stockage temporaire où ajouter les modifications avant de commettre (sauvegarde draft) )
- Local Repo, c'est l'endroit où les commits changes sont stockés, c'est une image du code modifié enregistré sur le local repo en attandant d'etre intégré dans le remote repo.
- Remote repo (git) : c'est un serveur comme github pour partager, sauvegarder et pouvoir recuperer le code. la commande git push permet d'envoyer l'ensemble des commits sur le repo distant. sur le repo distant les equipes souvent peuvent collaborer soit directement sur github ou bitbuket ou autre ..

=> la collaboration sur git est dans les deux sens, git push pour partager son avancement et git pull pour se synchroniser sut la dernière version en ligne er recupérer l'avancement de l'équipe également.

### Procédure :

1. connection à GitHub
2. créer un nouveau repo et le configurer
3. Cloner le repo sur le PC local pour connecter le repo distant au repo local (parfois cela demande de crée un token pour pouvoir se connecter, ou avoir une clé ssh pour ne plus rencotrer ce genre de problème)
4.

### les commandes Terminal et Git sur terminal :

#### Terminal :

- pour ouvrir un editeur sur un dossier, il fau faire cd sur le dossier souhaité puis la commande "code ."
-

#### GIT :

- "git clone "lien https" " pour copier une repo en local et pouvoir y traviller à distance. (reccuperer un projet via git)
-

# Règles à retenir :

1. Quand un problème est basé sur des règles fixes → mets-les dans un objet, pas dans des if, exemple :

```js
const rps = (p1, p2) => {
  var map = {
    rock: "scissors",
    scissors: "paper",
    paper: "rock",
  };

  if (p1 == p2) {
    return "Draw!";
  } else {
    return "Player " + (map[p1] == p2 ? 1 : 2) + " won!";
  }
};
```

au lieu de

```js
const rps = (p1, p2) => {
  if (p1 === p2) return "Draw!";
  var rules = { rock: "scissors", paper: "rock", scissors: "paper" };
  if (p2 === rules[p1]) {
    return "Player 1 won!";
  } else {
    return "Player 2 won!";
  }
};
```

2. Methode d'analyse de l'enoncé n'est pas liée au langage. pour pouvoir coder plus facilement, il fuadrait developper sa propre façon de decortiquer le problème pour savoir chercher en plus comment le résoudre selon le langage utilsié. donc créer un framework mental réutilisable partout en dev.
   exemple d'un problème :

```js
Task
You get an array of numbers, return the sum of all of the positives ones.

Example
[1, -4, 7, 12] => 1+7+12=20
Note
If there is nothing to sum, the sum is default to 0.
```

voci la méthode:

```js
1) 🧩 ÉTAPE 1 — Identifier la nature du problème

Pose-toi ces 4 questions, toujours dans cet ordre :

1️⃣ Est-ce une transformation ?

Est-ce que je reçois quelque chose et je dois produire autre chose ?

Ici :
✔️ tableau → nombre
👉 fonction obligatoire

2️⃣ Quel est le type des données en entrée ?

Primitif ? tableau ? objet ? string ?

✔️ Ici : array

3️⃣ Quel est le type de sortie ?

nombre ? string ? tableau ?

✔️ Ici : number

4️⃣ Est-ce un traitement unique ou répété ?

Dois-je examiner chaque élément ?

Ici :
✔️ oui → itération obligatoire

🧠 RÈGLE GÉNÉRALE

Dès que tu vois “array” + “condition” → boucle ou méthode d’array




🧩 ÉTAPE 2 — Traduire l’énoncé en verbes techniques

Énoncé :

"return the sum of all of the positives ones"

Traduction dev 👇

get an array =>	paramètre
positives	=> condition
sum	=> accumulation
return	=> return obligatoire
default to 0	=> valeur initiale

Pattern détecté automatiquement
👉 FILTER + REDUCE



🧩 ÉTAPE 3 — Scanner les outils du langage

Pose-toi cette question clé :

Est-ce que JavaScript a déjà une méthode pour ce pattern ?


Besoin	            Méthode
parcourir	        => for, forEach, map
filtrer	            => filter
additionner	        => reduce
condition simple	=> if




🧩 ÉTAPE 4 — Choisir la stratégie (du plus simple au plus expressif)

OPTION 1 — boucle simple (universelle)
function sumPositive(arr) {
  let sum = 0;

  for (let n of arr) {
    if (n > 0) {
      sum += n;
    }
  }

  return sum;
}


✔️ marche toujours
✔️ facile à débug
✔️ langage universel

OPTION 2 — méthode fonctionnelle (niveau intermédiaire)
function sumPositive(arr) {
  return arr
    .filter(n => n > 0)
    .reduce((sum, n) => sum + n, 0);
}


✔️ expressif
✔️ lisible
✔️ très demandé en interview



🧩 ÉTAPE 5 — Vérifier les cas limites (CRUCIAL)

Pose-toi toujours :

tableau vide ? → []

aucun positif ? → 0

valeurs négatives uniquement ? → 0

➡️ reduce(..., 0) protège automatiquement ✅
```
