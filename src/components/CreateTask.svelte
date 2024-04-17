<script>
    // import { createEventDispatcher } from "svelte";
    import { slide } from "svelte/transition";
    import { stasks } from "../store";
    import Color from "./Color.svelte";

    // const dispatch= createEventDispatcher()
    
    let title= ''
    let description= ''
    let color= ''

    function submitHandler(e) {
        if (!title) {
            alert("Please provide a title");
            return;
        }

        let id= (Math.random()* new Date().getTime()).toString()

        let task= {
            id,
            title,
            description,
            color,
            completed: false,
            editable: false,
        }
        // dispatch("taskCreated", task);
        let newTasks= [task, ...$stasks]
        stasks.set(newTasks)
        e.target.reset();
        color=""
    }

</script>

<div class="card card-body my-4" transition:slide>
    <form on:submit|preventDefault={submitHandler}>
        <div class="form-group">
            <label for="title">Enter a task title</label>
            <input type="text" placeholder="Task Title" id="title" class="form-control" bind:value={title}>
        </div>

        <div class="form-group">
            <label for="desc">Enter a short description</label>
            <textarea name="" id="desc" class="form-control" bind:value={description}></textarea>
        </div>

        <Color bind:selectedColor={color} />
        <input type="submit" value="Create Task" class="btn btn-primary my-4">
    </form>
</div>