<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    let searchTerm = "";
    
    const search = event =>{
        searchTerm = event.target.value;

        if (searchTerm) {
            dispatch('search', {
                searchTerm,
            })
        } else {
            dispatch('clearSearch', {});
        }
    }
</script>

<input 
    type="text"
    placeholder="Search movie"
    value={searchTerm}
    on:keyup={search}
/>