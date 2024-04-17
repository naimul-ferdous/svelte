<script>

    // import { createEventDispatcher } from 'svelte';
    
    // const dispatch= createEventDispatcher()


    export let greeting= 'Hello'
    export let mname= 'Naimul Ferdous'

    // function nameChangeHandler(e) {
    //     if (e.key==='Enter') {
    //         dispatch("nameChanged", name)
    //     }
    // }

</script>

<h1>{greeting}, {mname}</h1>

<!-- <input type="text" name="" id="" bind:value={name} on:keypress={nameChangeHandler} > -->
<input type="text" name="" id="" bind:value={mname} >