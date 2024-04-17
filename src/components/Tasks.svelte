<script context="module">
  import { slide } from "svelte/transition";
</script>

<script>
  import { stasks } from "../store";
  export let taskList = [];
  export let label = "ALL";
  


  $: totalComplete= $stasks.filter(t=> t.completed).length



  function toggleCheck(e, id) {
    let tempTasks= [...$stasks]
    let index= tempTasks.findIndex(t=> t.id===id)
    tempTasks[index].completed= e.target.checked;
    stasks.set(tempTasks);
  }

  function dblHandler(id) {
    let tempTasks= [...$stasks]
    let index= tempTasks.findIndex(t=> t.id===id)
    tempTasks[index].editable= true;
    stasks.set(tempTasks);
  }

  function updateTask(e, id) {


    if (e.key==="Enter" && e.target.value) {
      let tempTasks= [...$stasks]
      let index= tempTasks.findIndex(t=> t.id===id)
      tempTasks[index].title= e.target.value;
      tempTasks[index].editable= false;
      stasks.set(tempTasks);
    }
  }
</script>



<style>
  .complete {
    text-decoration: line-through;
  }

  .color {
    height: 5px;
  }
</style>

<div class="my-3" transition:slide >
  <h4>{label} Tasks</h4>
  {#if taskList.length === 0}
    <p>There is no Task</p>
  {:else}
    <p>Total Task: {$stasks.length} Active: {$stasks.length - totalComplete} Completed: {totalComplete}</p>
    <ul class="list-group">
      {#each taskList as task}
        <li class="list-group-item" on:dblclick={e=> dblHandler(task.id)}>
          <input
            type="checkbox"
            name=""
            id=""
            class="form-check-input"
            checked={task.completed}
            on:change={(e)=> toggleCheck(e, task.id)}
          />
          <label for="">
            {task.completed ? "Done!!!" : "Not Yet Done!"}
          </label>
          <input
            type="text"
            name=""
            id=""
            bind:value={task.title}
            disabled={!task.editable}
            class="{task.completed ? "form-control complete":"form-control"}"
            on:keypress={(e)=> updateTask(e, task.id)}
          />
          <div class="color mx-3" title={task.description} style="background: {task.color};">

          </div>
        </li>
      {/each}
    </ul>
  {/if}
</div>
