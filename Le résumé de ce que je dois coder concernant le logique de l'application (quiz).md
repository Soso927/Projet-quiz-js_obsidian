Absolument. Tu vas t’occuper de la **logique du quiz**, c’est-à-dire toute la partie en JavaScript qui fait fonctionner l'application. Tu n’as pas besoin de te préoccuper du design (HTML/CSS), juste de comment les données sont traitées et les actions se déroulent.

---

## ✅ **Voici précisément ce que tu dois faire (étape par étape)**

---

### 1. **Définir les données du quiz**

Tu dois créer une **structure de données** pour contenir toutes les questions, leurs réponses, et leur type.

#### Exemple :

```js
const questions = [
  {
    question: "Quelle est la capitale de la France ?",
    type: "multiple",
    choices: ["Paris", "Lyon", "Marseille", "Nice"],
    answer: "Paris"
  },
  {
    question: "Le soleil est une étoile.",
    type: "boolean",
    answer: true
  },
  {
    question: "Quel est ton prénom ?",
    type: "text",
    answer: "Jean"
  }
];
```

Tu peux proposer plusieurs types :

- `multiple` : choix dans une liste
    
- `boolean` : vrai/faux
    
- `text` : champ à remplir
    

---

### 2. **Afficher une question à la fois**

Tu dois créer une fonction pour **afficher la question actuelle**. Par exemple :

```js
let currentQuestionIndex = 0;

function showQuestion() {
  const question = questions[currentQuestionIndex];
  
  // Tu peux appeler une fonction de ton binôme ici pour afficher la question
  // Exemple :
  console.log("Question : " + question.question);
  if (question.type === "multiple") {
    console.log("Choix : " + question.choices.join(", "));
  }
}
```

---

### 3. **Réception et vérification de la réponse de l'utilisateur**

Tu dois créer une fonction appelée quand l'utilisateur répond (par un bouton ou un champ texte) :

```js
let score = 0;

function submitAnswer(userAnswer) {
  const question = questions[currentQuestionIndex];
  let isCorrect = false;

  if (question.type === "text") {
    isCorrect = userAnswer.trim().toLowerCase() === question.answer.toLowerCase();
  } else {
    isCorrect = userAnswer === question.answer;
  }

  if (isCorrect) {
    score++;
  }

  currentQuestionIndex++;
  if (currentQuestionIndex < questions.length) {
    showQuestion();
  } else {
    endQuiz();
  }
}
```

Ton binôme devra appeler `submitAnswer()` avec la réponse donnée par l’utilisateur (il récupérera la valeur depuis le DOM).

---

### 4. **Afficher le score à la fin**

Tu dois ajouter une fonction simple :

```js
function endQuiz() {
  console.log("Quiz terminé !");
  console.log("Score final : " + score + "/" + questions.length);
  // Ton binôme pourra afficher ça sur la page
}
```

---

### 5. (Optionnel) **Ajouter un chronomètre**

```js
let timeLeft = 60;
let timer = setInterval(() => {
  timeLeft--;
  // Mettre à jour l'affichage du chrono (ton binôme le fera)
  if (timeLeft <= 0) {
    clearInterval(timer);
    endQuiz();
  }
}, 1000);
```

---

## 🛠️ Résumé de ce que tu vas coder :

|Fonction|À quoi elle sert|
|---|---|
|`questions`|Contient les données du quiz|
|`showQuestion()`|Affiche la question actuelle|
|`submitAnswer()`|Vérifie la réponse, gère le score, passe à la suivante|
|`endQuiz()`|Termine le quiz et montre le score|
|(optionnel) `timer`|Gère un compte à rebours|

---

