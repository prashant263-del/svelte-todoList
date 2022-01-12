<script>
    export let todos = [];
    export let t;
    let newTodoName = ''

    $: totalTodos = todos.length
    $: completedTodos = todos.filter(todo => todo.completed).length

    function removeTodo(todo) {
        todos = todos.filter(t => t.id !== todo.id)
    }

    // $: console.log('newTodoName: ', newTodoName)
    function addTodo() {
        todos = [...todos, { id: newTodoId, name: newTodoName, completed: false }]
        newTodoName = ''
    }
    
    let newTodoId
    $: {
        if (totalTodos === 0) {
        newTodoId = 1;
        } else {
        newTodoId = Math.max(...todos.map(t => t.id)) + 1;
        }
    }

  </script>
  

<h1>Svelte To-Do list</h1>
<!-- Todos.svelte -->
<div class="todoapp stack-large">

    <!-- NewTodo -->
    <form on:submit|preventDefault={addTodo}>
        
        <h2 class="label-wrapper">
            <label for="todo-0" class="label__lg">
                What needs to be done? {t}
            </label>
        </h2>
        <!-- <input type="text" id="todo-0" autocomplete="off"
        class="input input__lg" /> -->
        <!-- <input value={newTodoName} on:keydown={(e) => newTodoName = e.target.value} id="todo-0" autocomplete="off" class="input input__lg" /> -->
        <!-- <input bind:value={newTodoName} /> -->
        <input bind:value={newTodoName} type="text" id="todo-0" autocomplete="off" class="input input__lg" />
      <button type="submit" disabled="" class="btn btn__primary btn__lg">
        Add
      </button>
    </form>
  
    <!-- Filter -->
    <div class="filters btn-group stack-exception">
      <button class="btn toggle-btn" aria-pressed="true">
        <span class="visually-hidden">Show</span>
        <span>All</span>
        <span class="visually-hidden">tasks</span>
      </button>
      <button class="btn toggle-btn" aria-pressed="false">
        <span class="visually-hidden">Show</span>
        <span>Active</span>
        <span class="visually-hidden">tasks</span>
      </button>
      <button class="btn toggle-btn" aria-pressed="false">
        <span class="visually-hidden">Show</span>
        <span>Completed</span>
        <span class="visually-hidden">tasks</span>
      </button>
    </div>
  
    <!-- TodosStatus -->
    <h2 id="list-heading">{completedTodos} out of {totalTodos} items completed</h2>
    
    <!-- Todos -->
<!-- Todos -->
<ul role="list" class="todo-list stack-large" aria-labelledby="list-heading">
    {#each todos as todo (todo.id)}
      <li class="todo">
        <div class="stack-small">
          <div class="c-cb">
            <!-- <input type="checkbox" id="todo-{todo.id}" checked={todo.completed}/> -->
            <input type="checkbox" id="todo-{todo.id}" on:click={() => todo.completed = !todo.completed}
                checked={todo.completed}/>

            <label for="todo-{todo.id}" class="todo-label">
              {todo.name}
            </label>
          </div>
          <div class="btn-group">
            <button type="button" class="btn">Edit <span class="visually-hidden">{todo.name}</span>
            </button>
            <button type="button" class="btn btn__danger" on:click={() => removeTodo(todo)}          >
                Delete <span class="visually-hidden">{todo.name}</span>
             </button>          
          </div>
        </div>
      </li>
    {:else}
      <li>Nothing to do here!</li>
    {/each}
  </ul>
  
        
    <!-- </ul> -->
  
    <hr />
  
    <!-- MoreActions -->
    <div class="btn-group">
      <button type="button" class="btn btn__primary">Check all</button>
      <button type="button" class="btn btn__primary">Remove completed</button>
    </div>
  
  </div>
  