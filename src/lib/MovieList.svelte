<script>

    export let movies;
</script>

<ul>
    
    
    {#each movies as movie (movie.title)}
    <div>
        <h3>{movie.title}</h3>
        <h4>{movie.rating}⭐</h4>
    </div>
    <!-- {#each movie.rating as rating, i}
        <i>⭐</i>
    {/each} -->
    {/each}
</ul>