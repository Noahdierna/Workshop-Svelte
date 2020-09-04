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
            <li>{todo.name}</li>
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
créons la fonction addTodo 

```
      function addTodo (){
            todos=[...todos,{
                  name:newTodo,
                  completed:false
            }]
            newTodo =''
      }
```

maintenant, nous pouvons ajouter des tâches mais passons à la partie principale de la todo list : pouvoir cocher si la tâche est finie ou pas.

Pour cela nous allons ajouter un input checkbox dans le li 

```
<li>
	<input type='checkbox' bind:checked={todo.completed}>
	{todo.name}
</li>
```

ainsi qu'un label en dessous de notre h1 avec une checkbox qui nous permettra de filtrer les tâches.

```
<h1>
	Ma liste de tâches
</h1>
<label><input type='checkbox' bind:checked={showCompleted}> Afficher les tâches finies </label>

```

et on déclare la variable showCompleted a true 

```
let showCompleted =true
```
Pour pouvoir filtrer les tâches finies nous allons créer une variable filteredTodo 

```
let filterdTodos = todos.filter(t=> t.completed ===false)
```
cela nous donne une nouvelle liste que l'on pourra utiliser à la place de todos dans notre {#each}

```
	{#each filterdTodos as todo}
```

ça devrait normalement marcher mais malheureusement il va falloire changer quelques variables dans le code pour rendre tout cela reactif.

notre variable filteredTodo n'est pas réactive donc nous allons utiliser un élément de la syntaxe de Svelte  le ``` $: ``` 

```
	$: filterdTodos = todos.filter(t=> t.completed ===false)
```

le ``` $: ``` devant une variable veut dire que cette dernière dépendra des choses utilisées pour la générer. ici on parle de todos.

On vaégalement changer le bind:checked de la checkbox des tâches en créant une fonction qui detectera le changement 

```
	<input type='checkbox' on:change:{() => changeTodo(todo)} >
 ```

 et la fonction changeTodo 

  ```
  	function changeTodo (todo){
		todos = todos.map(t=>{
			if (t=== todo) {
				return {...todo,completed: !t.completed}
			}
			return t 
		})
	}
 ```

dans filteredTodo il va falloire déclarer que si showCompleted est true on ne filtre aucune valeur  sinon les tâches qui ne sont pas cochées 

```
$: filterdTodos = todos.filter(t=> showCompleted === true ? true :  t.completed ===false)
```

et pour finir, gardons la valeurs de la checkbox de nos tâches 

```
	<input type='checkbox' checked={todo.completed} on:change={() =>changeTodo(todo)}>
```

Bravo ! Vous avez réalisé votre première application avec Svelte ! 