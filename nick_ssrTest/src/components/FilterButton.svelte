<script>
  export let filter = 'all';
  //export let onclick = (clicked) => {};
  //$: onclick(filter);
</script>

<div class="filters btn-group stack-exception">
    <button class="btn toggle-btn" class:btn__primary={filter === 'all'} aria-pressed={filter === 'all'} on:click={()=> filter = 'all'}>
      <span class="visually-hidden">Показать</span>
      <span>Все</span>
      <span class="visually-hidden">задачи</span>
    </button>
    <button class="btn toggle-btn" class:btn__primary={filter === 'active'} aria-pressed={filter === 'active'} on:click={()=> filter = 'active'}>
      <span class="visually-hidden">Показать</span>
      <span>Активные</span>
      <span class="visually-hidden">задачи</span>
    </button>
    <button class="btn toggle-btn" class:btn__primary={filter === 'completed'} aria-pressed={filter === 'completed'} on:click={()=> filter = 'completed'}>
      <span class="visually-hidden">Показать</span>
      <span>Выполненные</span>
      <span class="visually-hidden">задачи</span>
    </button>
  </div>