Pour créer un formulaire de type quiz en utilisant des questions stockées dans un fichier JSON, voici comment tu pourrais procéder.

### 1. Structure du fichier `questions.json`

Commence par créer un fichier `questions.json` où tu stockes tes questions et les options de réponse. Voici un exemple de structure de ce fichier :

```json
[
  {
    "question": "Quelle est la capitale de la France ?",
    "options": ["Paris", "Lyon", "Marseille", "Toulouse"],
    "correct": 0
  },
  {
    "question": "Quel est le plus grand océan ?",
    "options": ["Atlantique", "Pacifique", "Indien", "Arctique"],
    "correct": 1
  },
  {
    "question": "Combien de continents y a-t-il ?",
    "options": ["5", "6", "7", "8"],
    "correct": 2
  }
]
```

### 2. Code HTML, JavaScript et CSS pour afficher le quiz

Voici un exemple de code qui lit le fichier `questions.json`, affiche les questions sous forme de boutons radio ou de checkboxes, et permet de calculer le score à la fin.

#### Structure HTML de base

Crée un fichier HTML (par exemple, `index.html`) avec le formulaire de quiz :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quiz</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }
    .question {
      margin-bottom: 20px;
    }
    .options {
      margin-left: 20px;
    }
    .result {
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <h1>Quiz</h1>
  <form id="quiz-form"></form>
  <button id="submit-button" type="button">Soumettre</button>
  <div id="result" class="result"></div>

  <script src="quiz.js"></script>
</body>
</html>
```

#### Code JavaScript pour charger les questions et gérer le quiz (`quiz.js`)

Ce fichier JavaScript chargera les questions depuis le fichier JSON, affichera les options sous forme de boutons radio et calculera le score une fois le quiz soumis.

```javascript
// Charger le fichier JSON avec les questions
fetch('questions.json')
  .then(response => response.json())
  .then(data => {
    // Ajouter les questions au formulaire
    const quizForm = document.getElementById('quiz-form');
    data.forEach((questionData, index) => {
      // Créer une section pour chaque question
      const questionContainer = document.createElement('div');
      questionContainer.classList.add('question');
      
      // Ajouter la question
      const questionText = document.createElement('p');
      questionText.textContent = `${index + 1}. ${questionData.question}`;
      questionContainer.appendChild(questionText);
      
      // Ajouter les options sous forme de boutons radio
      const optionsContainer = document.createElement('div');
      optionsContainer.classList.add('options');
      questionData.options.forEach((option, i) => {
        const label = document.createElement('label');
        
        // Créer un bouton radio pour chaque option
        const radioInput = document.createElement('input');
        radioInput.type = 'radio';
        radioInput.name = `question${index}`;
        radioInput.value = i;
        
        label.appendChild(radioInput);
        label.appendChild(document.createTextNode(option));
        optionsContainer.appendChild(label);
        optionsContainer.appendChild(document.createElement('br'));
      });

      questionContainer.appendChild(optionsContainer);
      quizForm.appendChild(questionContainer);
    });

    // Ajouter un gestionnaire d'événements pour le bouton de soumission
    document.getElementById('submit-button').addEventListener('click', () => {
      let score = 0;
      
      // Vérifier les réponses de l'utilisateur
      data.forEach((questionData, index) => {
        const selectedOption = document.querySelector(`input[name="question${index}"]:checked`);
        if (selectedOption && parseInt(selectedOption.value) === questionData.correct) {
          score++;
        }
      });
      
      // Afficher le score
      const resultContainer = document.getElementById('result');
      resultContainer.textContent = `Votre score : ${score} / ${data.length}`;
    });
  })
  .catch(error => {
    console.error('Erreur de chargement du fichier JSON:', error);
  });
```

### Explication du Code

1. **Fichier JSON** (`questions.json`) :
    
    - Contient les questions et leurs options de réponse.
        
    - Chaque question a une clé `question` pour le texte de la question, une clé `options` pour les choix de réponses, et une clé `correct` qui indique l'indice de la réponse correcte.
        
2. **HTML** (`index.html`) :
    
    - Contient la structure de base du formulaire avec un bouton pour soumettre les réponses.
        
    - Un élément `<form>` avec un identifiant `quiz-form` pour contenir les questions et les options.
        
3. **JavaScript** (`quiz.js`) :
    
    - Le fichier JSON est chargé avec la méthode `fetch`.
        
    - Les questions et options sont ajoutées dynamiquement au DOM.
        
    - Lorsqu'on clique sur le bouton "Soumettre", le script vérifie les réponses sélectionnées et calcule le score.
        

### 3. Tester le projet

1. **Serveur local** : Si tu utilises un environnement de développement local (comme **Laragon**), place le fichier `questions.json`, `index.html`, et `quiz.js` dans le dossier approprié.
    
2. **Ouvrir dans le navigateur** : Accède à `index.html` dans ton navigateur pour voir le quiz en action.
    

### Conclusion

Ce code charge dynamiquement les questions à partir d'un fichier JSON et crée un quiz interactif avec des boutons radio. Tu peux facilement étendre ce code en ajoutant plus de questions, en personnalisant l'apparence avec CSS, ou en ajoutant des fonctionnalités supplémentaires (par exemple, afficher les réponses après la soumission, minuter le quiz, etc.).