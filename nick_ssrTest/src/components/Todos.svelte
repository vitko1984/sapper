<!-- Todos.svelte -->
<div class="todoapp stack-large">

    <!-- NewTodo -->
    <NewTodo autofocus on:addTodo={e => addTodo(e.detail)} />
  
    <!-- Filter -->
    <!--<FilterButton {filter} onclick={ (clicked) => filter = clicked } />-->
    <FilterButton bind:filter /> 
  
    <!-- TodosStatus -->
    <TodosStatus bind:this={todosStatus} {todos} />
  
    <!-- Todos -->
    <ul role="list" class="todo-list stack-large" aria-labelledby="list-heading">
      {#each filterTodos(filter, todos) as todo (todo.id)}
      <li class="todo">
        <Todo {todo} on:remove={e => removeTodo(e.detail)} on:update={e => updateTodo(e.detail)} />
      </li>
      {:else}
        <li>Здесь нечего делать!</li>
      {/each}
    </ul>
  
    <hr />
  
    <!-- MoreActions -->
    <MoreActions {todos}
      on:checkAll={e => checkAllTodos(e.detail)}
      on:removeCompleted={removeCompletedTodos} />
  </div>

  <script>
    import FilterButton from './FilterButton.svelte';
    import Todo from './Todo.svelte';
    import MoreActions from './MoreActions.svelte';
    import NewTodo from './NewTodo.svelte';
    import TodosStatus from './TodosStatus.svelte';

    import { alert } from '../stores/store.js';

    export let todos = [];
    //let newTodoName = '';
    let newTodoId;
    let todosStatus;                   // reference to TodosStatus instance
    $: todos.length ? Math.max(...todos.map(t => t.id)) + 1 : 1;

    function removeTodo(todo) {
      todos = todos.filter(t => t.id !== todo.id);
      todosStatus.focus();             // give focus to status heading
      $alert = `Todo '${todo.name}' has been deleted`
    };

    function updateTodo(todo) {
      const i = todos.findIndex(t => t.id === todo.id)
      if (todos[i].name !== todo.name) $alert = `todo '${todos[i].name}' has been renamed to '${todo.name}'`
      if (todos[i].completed !== todo.completed)  $alert = `todo '${todos[i].name}' marked as ${todo.completed ? 'completed' : 'active'}`
      todos[i] = { ...todos[i], ...todo }
    };
    function addTodo(name) {
      todos = [...todos, { id: newTodoId, name, completed: false }];
      $alert = `Todo '${name}' has been added`;
    };
    const checkAllTodos = (completed) => {
      todos = todos.map(t => ({...t, completed}))
      $alert = `${completed ? 'Отметка' : 'Отмена отметки'} ${todos.length} задач`
    };

    const removeCompletedTodos = () => {
      $alert = `Удалить ${todos.filter(t => t.completed).length} задачи`
      todos = todos.filter(t => !t.completed)  
    };

    let filter = 'all';
    const filterTodos = (filter, todos) => 
    filter === 'active' ? todos.filter(t => !t.completed) :
    filter === 'completed' ? todos.filter(t => t.completed) : 
    todos;

    $: {
      if (filter === 'all')               $alert = 'Browsing all todos'
      else if (filter === 'active')       $alert = 'Browsing active todos'
      else if (filter === 'completed')    $alert = 'Browsing completed todos'
    };
    /*const filterTodos = (filter, todos) =>
    filter === 'active' ? todos.filter(t => !t.completed) :
    filter === 'completed' ? todos.filter(t => t.completed) :
    todos;*/
  </script>