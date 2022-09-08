<script>
  let todoItems = [];
  let newTodo = '';

  export let backgroundColor="blue"; 

  function addTodo() {
    newTodo = newTodo.trim();
    if (!newTodo) return;

    const todo = {
      text: newTodo,
      checked: false,
      id: Date.now(),
    };

    todoItems = [...todoItems, todo];
    newTodo = '';
  }

  function toggleDone(id) {
    const index = todoItems.findIndex(item => item.id === Number(id));
    todoItems[index].checked = !todoItems[index].checked;
  }

  function deleteTodo(id) {
    todoItems = todoItems.filter(item => item.id !== Number(id));
  }

  function deleteAllTodos() {
    todoItems = [];
  }

</script>

<main style="background-color:{backgroundColor}">
  <div class="container">
    <ul class="todo-list">
      {#each todoItems as todo (todo.id)}
        <li class="todo-item {todo.checked ? 'done' : ''}">
          <input id={todo.id} type="checkbox" />
          <label for={todo.id} class="tick" on:click={() => toggleDone(todo.id)}></label>
          <span>{todo.text}</span>
          <button class="delete-todo" on:click={() => deleteTodo(todo.id)}>
            <svg><use href="#delete-icon"></use></svg>
          </button>

          
        </li>
      {/each}
    </ul>
    <div class="empty-state">
      <svg class="checklist-icon"><use href="#checklist-icon"></use></svg>
      <h3>Ajoute ta première todo-list</h3>
      
    </div>
    <form on:submit|preventDefault={addTodo}>
      <input class="js-todo-input" type="text" aria-label="Entrez un nouveau todo" placeholder="" bind:value={newTodo}>
    </form>
    <button on:click={() => addTodo()}>Ajouter</button>
    <button on:click={() => deleteAllTodos()}>Supprimer tout</button>
    
  </div>
</main>


<style>
  main {
    font-size: 30px;
    text-align: center;
    background-color:"{backgroundColor}:black";
  }

 * {
    background-color: white;
  }

  button {
    font-size: 20px;
    background-color: black;
    color: white;
    border-radius: 5px;
  }

  input {
    font-size: 20px;
  }
  h3{
    font-family: Arial;
  }
</style>