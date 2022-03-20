<script>
    import { createEventDispatcher } from 'svelte';
    //There's a shorthand for this i think
    const dispatch = createEventDispatcher();
    
    let title="";
    let rating = "1";

    const onTitleChange = e => {
        title = e.target.value
    } 

    const onRatingSelect = e => {
        rating = e.target.value;
    }

    const submitMovie = () => {
        if (title) {
            //"submitMovie is what we are calling the event"
            dispatch('submitMovie', {
                movie: {
                    title,
                    rating,
                }
            })
            //Reset input
            title=""
            rating="1"
        }
    }
</script>


<h2 hidden={!title}>{title}</h2>
<h3 hidden={!rating}>{rating}⭐</h3>
<input 
    type="text" 
    placeholder="Movie Title" 
    value="{title}" 
    on:keyup={onTitleChange}
/>


<select value="rating" on:change={onRatingSelect}>
    <option value="1">1</option>
    <option value="2">2</option>
    <option value="3">3</option>
    <option value="4">4</option>
    <option value="5">5</option>
</select>

<button disabled={!title} on:click={submitMovie}>Submit</button>