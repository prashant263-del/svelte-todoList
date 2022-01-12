<script>
  import Todos from './components/Todos.svelte'

  let todos = [
    { id: 1, name: 'Create a Svelte starter app', completed: true },
    { id: 2, name: 'Create your first component', completed: true },
    { id: 3, name: 'Complete the rest of the tutorial', completed: false },
    { id: 4, name: 'This is my task', completed: false }
  ];

  let test = 'Svelte test';

</script>

<Todos todos={todos} t={test} />
