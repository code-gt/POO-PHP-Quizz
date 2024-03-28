# QCM POO 📋

## 🚀 PARTIE 1

### 📌 Description
Afin d’utiliser la POO PHP dans un cas concret, essayons de réaliser un TP type Quiz avec des class. Pour cette première partie, pas besoin de base de données (rien ne sera enregistré), mais vous devrez réfléchir aux propriétés et méthodes de vos class.

Vous aurez besoin de trois classes :
- Qcm
- Question
- Answer

De sortes que :
- Un QCM regroupe l’ensemble des questions composant le quiz et la méthode qui permet d’afficher toutes les questions dans notre HTML.
- Une Question contient un corps sous forme de texte et plusieurs Answers ainsi que l’explication de la bonne réponse.
- Une Answer contient un texte ainsi que l'attribut permettant d’identifier si c’est une bonne réponse.

Vous n’aurez pas besoin de l’héritage. On l’utilise lorsque avec des **classes A et B, on peut dire que B est un A**. Or ici une réponse n'est pas une question, une question n'est pas un Qcm.

### 🌳 Arborescence
Vous organiserez vos fichiers ainsi :
- Un dossier `class` contenant vos 3 classes
- Un dossier `config` qui ne contient rien pour le moment
- Le fichier `index.php` à la racine

### ⚙️ Fonctionnalités requises
- Ajouter une question
    - Pouvoir ajouter les réponses possibles à une question
    - Pouvoir définir la bonne réponse comme telle
- Pouvoir définir les explications de la réponse d'une question.

Il doit être possible de faire ceci pour générer un Qcm :
```php
$qcm = new Qcm();
$question1 = new Question('POO signifie :');
$question1->addAnswer(new Answer('Php Orienté Objet'));
$question1->addAnswer(new Answer('ProgrammatiOn Orientée Outil'));
$question1->addAnswer(new Answer('Programmation Orientée Objet', Answer::BONNE_REPONSE));
$question1->addAnswer(new Answer('Papillon Onirique Ostentatoire'));
$question1->setExplications('Sans commentaires si vous avez eu faux :-°');
$qcm->addQuestion($question1);
$qcm->generate();
```

## 🚀 PARTIE 2

### 📌 Description

Vous avez réussi à créer vos 3 classes ? Parfait, essayons d’utiliser PDO dans nos objets maintenant. Voici la liste des modifications à apporter.

#### 📋 QCM

QCM doit devenir notre Manager, il contiendra en plus une instance de PDO dans une private `$db` qui sera initialisé dans son constructeur. Nous allons créer une nouvelle méthode public `getQuestions()` qui utilisera une requête PDO pour récupérer les questions de la base de données de votre quiz. La fonction `generate()` reste inchangée.

#### ❓ Question

Nous devons transformer cette classe en une “Entité”, c'est-à-dire qu’elle doit avoir autant de propriétés qu’il y a de colonnes dans votre table (avec les accesseurs et mutateurs correspondants).

#### ✏️ Answer

Vous allez devoir créer une table `answer` et extraire les réponses de votre table `question`. Ensuite, vous devez appliquer le même traitement à cette classe que pour la classe Question (en faire une Entité).

La fonction `getQuestions()` ne doit que gérer la requête SQL, créez une nouvelle private function qui fonctionnera ainsi :
- Recevoir en argument le tableau de données récupéré par la requête
- Instancier les objets Question et Answer avec ce tableau
- Cette nouvelle fonction sera appelée par `getQuestion()`

Il doit être possible de faire ceci pour générer un Qcm :
```php
$db = new PDO();
$qcm = new Qcm($db);
$qcm->getQuestions();
$qcm->generate();
```

### ⚠️ ATTENTION !

Nous n’implémentons pas la logique du traitement des réponses dans ce TP. Le but de ce TP est de vous familiariser avec une nouvelle logique, donc on y va pas à pas. 🚀
