<script context="module">
  import CreateTask from "./components/CreateTask.svelte";
  import Tasks from "./components/Tasks.svelte";
  import TopButtons from "./components/TopButtons.svelte";
  import { stasks } from "./store";
</script>

<script>
  let toggleCreateTaskForm = false;
  let toggleTaskList = true;
  let filter = "all";
  $: activeTasks = $stasks.filter((t) => !t.completed);
  $: completedTasks = $stasks.filter((t) => t.completed);
</script>

<svelte:head>
  <link
    href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
    rel="stylesheet"
    integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH"
    crossorigin="anonymous"
  />
  <title>Svelte Practice</title>
</svelte:head>

<div class="container">
  <div class="row">
    <div class="col-md-6 offset-md-3 my-4">
      <h1 class="display-4">Hello Catians</h1>
      <TopButtons
        bind:showForm={toggleCreateTaskForm}
        bind:showList={toggleTaskList}
        bind:filter
      />
      {#if toggleCreateTaskForm}
        <CreateTask />
      {/if}
      {#if toggleTaskList}
        {#if filter==='all'}
          <Tasks taskList={$stasks} label="All" />
        
        {:else if filter==='active'}
          <Tasks taskList={activeTasks} label="Active" />
       
        {:else if filter==='completed'}
          <Tasks taskList={completedTasks} label="Completed" />
        {/if}
      {/if}
    </div>
  </div>
</div>
