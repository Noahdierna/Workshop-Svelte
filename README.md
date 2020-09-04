# Workshop-Svelte

Dans ce workshop, vous apprendrez à réaliser la célèbre 'To do list' en utilisant **Svelte**.

Pour ce faire, je vous donne rendez-vous sur le site officiel Svelte.dev dans le REPL qui nous permettra de tester du code sans passer par votre éditeur de texte.

Un fichier .Svelte se compose d'une partie ```<script> </script> ```où comme vous vous en doutez, nous pourrons y insérer nos variables, fonctions (etc..), une partie ```<style> </style>``` pour le css et ce que vous écrirez hors de ces 2 balises sera du html.

Pour commencer, nous allons créer un tableau 'todos' qui prendra  "name:'ma première tâche' " et " completed: false " 

ensuite dans l'HTML nous allons créer un titre H1 "MA liste de tâches" 

et des ul  afin de lister notre tableau.

Pour ce faire, nous allons untiliser la syntax de svelte pour boucler des ```<li>```

ce qui va nous donner : 
```
<ul>
      {#each todos as todo}
            <li>todo.name</li>
      {/each}
</ul>
```

Comme toute Todo list qui se respecte, nous allons créer un input afin d'y ajouter des tâches.

```<input type='text bind:value={newTodo}> ``` 

vous avez compris qu'on met entre '{}' des variables et puisque newTodo n'existe pas encore, on va la déclarer.

```let newTodo ='' ```

on crée le button Ajouter afin d'ajouter une li sur base de ce qu'on a rentré dans l'input et un bouton avec une fonction qui permettra de créer une nouvelle tâche

```
<input type='text' bind:value={newTodo}> 
<button on:click={addTodo}>
      Ajouter
<button>
```

