<script>
  import Todos from '../components/Todos.svelte';

  let todos = [
      {
        id: 1, name: 'Создайте стартовое приложение Svelte', completed: true
      },
      {
        id: 2, name: 'Создайте свой первый компонент', completed: true
      },
      {
        id: 3, name: 'Завершите оставшуюся часть учебника', completed: false
      }
    ];
</script>

<svelte:head>
	<title>Sapper To-Do list</title>
</svelte:head>

<Todos {todos} />
