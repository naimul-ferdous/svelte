<script>
  export let showForm = false;
  export let showList = true;
  export let filter = "all";
  import { stasks } from "../store";

  function changeFilter(filterName) {
    filter = filterName;
  }

  function clearTask() {
    let tempTasks= $stasks.filter(t=> !t.completed)
    stasks.set(tempTasks)
  }
</script>

<div>
  <button on:click={() => (showForm = !showForm)} class="btn btn-success btn-sm"
    >Create</button
  >
  <button
    on:click={() => (showList = !showList)}
    class="btn btn-warning btn-sm"
  >
    {showList ? "Hide" : "Show"}
  </button>
  <button on:click={()=> changeFilter("all")} class="btn btn-secondary btn-sm">ALL</button>
  <button on:click={()=> changeFilter("active")} class="btn btn-secondary btn-sm">Active</button>
  <button on:click={()=> changeFilter("completed")} class="btn btn-secondary btn-sm">Completed</button>
  <button class="btn btn-danger btn-sm" on:click={clearTask}>Clear</button>
</div>
