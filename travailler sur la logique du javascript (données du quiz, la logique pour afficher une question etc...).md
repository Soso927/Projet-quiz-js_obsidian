Parfait ! Un **quiz sur le développement web** est un super thème. Je vais te créer une base de fichier `script.js` avec des **questions types en HTML, CSS et JavaScript**, et la logique complète du quiz que **tu peux brancher facilement à l’interface de ton binôme**.

---

## ✅ Voici ce que contient ce script :

- Données du quiz (questions/réponses)
    
- Logique pour afficher une question
    
- Logique pour soumettre une réponse
    
- Calcul du score
    
- Fin du quiz
    

---

### 🧠 Fichier `script.js` – Logique du quiz

```js
// 1. Données du quiz
const questions = [
  {
    question: "Quel élément HTML est utilisé pour insérer du JavaScript dans une page ?",
    type: "multiple",
    choices: ["<javascript>", "<js>", "<script>", "<code>"],
    answer: "<script>"
  },
  {
    question: "Le CSS permet de structurer le contenu d'une page.",
    type: "boolean",
    answer: false // C'est HTML qui structure, CSS qui stylise
  },
  {
    question: "Quelle propriété CSS permet de changer la couleur du texte ?",
    type: "text",
    answer: "color"
  },
  {
    question: "Quelle méthode JavaScript permet d’ajouter un élément à la fin d’un tableau ?",
    type: "multiple",
    choices: ["push()", "pop()", "shift()", "append()"],
    answer: "push()"
  },
  {
    question: "Un identifiant en CSS commence par le symbole #.",
    type: "boolean",
    answer: true
  }
];

// 2. Variables d’état
let currentQuestionIndex = 0;
let score = 0;

// 3. Affichage de la question actuelle
function showQuestion() {
  const question = questions[currentQuestionIndex];
  const container = document.getElementById("question-container");

  // Nettoyer le contenu précédent
  container.innerHTML = "";

  // Titre de la question
  const questionEl = document.createElement("h2");
  questionEl.textContent = question.question;
  container.appendChild(questionEl);

  // Selon le type, afficher des boutons ou un champ texte
  if (question.type === "multiple") {
    question.choices.forEach(choice => {
      const btn = document.createElement("button");
      btn.textContent = choice;
      btn.onclick = () => submitAnswer(choice);
      container.appendChild(btn);
    });
  } else if (question.type === "boolean") {
    ["true", "false"].forEach(val => {
      const btn = document.createElement("button");
      btn.textContent = val;
      btn.onclick = () => submitAnswer(val === "true");
      container.appendChild(btn);
    });
  } else if (question.type === "text") {
    const input = document.createElement("input");
    input.type = "text";
    input.id = "text-answer";
    container.appendChild(input);

    const btn = document.createElement("button");
    btn.textContent = "Valider";
    btn.onclick = () => {
      const userInput = document.getElementById("text-answer").value;
      submitAnswer(userInput);
    };
    container.appendChild(btn);
  }
}

// 4. Traitement de la réponse
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

// 5. Fin du quiz
function endQuiz() {
  const container = document.getElementById("question-container");
  container.innerHTML = `
    <h2>Quiz terminé !</h2>
    <p>Ton score : ${score} / ${questions.length}</p>
  `;
}

// 6. Lancer le quiz au chargement
window.onload = showQuestion;
```

---

### 📄 Ce dont ton binôme a besoin dans `index.html` :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Quiz Dev Web</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Quiz Développement Web</h1>
  <div id="question-container"></div>

  <script src="script.js"></script>
</body>
</html>
```

---

Souhaitez-vous aussi :

- Un chronomètre avec un compte à rebours ?
    
- L’ajout de plusieurs thèmes (HTML, CSS, JS séparés) ?
    
- Une version avec score enregistré dans `localStorage` ?
    

Je peux t’aider à ajouter tout ça étape par étape. Tu veux continuer dans ce sens ?