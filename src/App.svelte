<script>
  import logo from './assets/svelte.png'
  import Counter from './lib/Counter.svelte'
  import Movieinput from './lib/Movieinput.svelte';
  import MovieList from  './lib/MovieList.svelte';
  import Search from './lib/Search.svelte';


  let movies = localStorage.getItem('movies') ? 
  JSON.parse(localStorage.getItem('movies')):
  [];
  //Or use the nullish operator ||
  

  const submitMovie = movie => {
    
    const newMovies = [...movies, movie ];
    localStorage.setItem('movies', JSON.stringify(newMovies))
    movies = newMovies;
  }

  const clearSearch = () => {
    movies = localStorage.getItem('movies') ? 
      JSON.parse(localStorage.getItem('movies')):
      [];
  }

  const search = searchTerm => {
    //This seems costly, probably better to check if array is empty
    const tempMovies = movies = localStorage.getItem('movies') ? 
      JSON.parse(localStorage.getItem('movies')):
      [];
    // Filter returns an array with all elements that passes the test
    //For each m (movie), if it includes the seach term, include it in the array
    movies = tempMovies.filter(m =>
     m.title.toLowerCase().includes(searchTerm.toLowerCase()))
  }

</script>

<div class="main">

  <h1>Movie Journal</h1>
  
  <!-- event.detail give us the data from the event object -->
  
   
   <MovieList movies={movies} />
   <Search 
   on:clearSearch={clearSearch} 
   on:search={event => search(event.detail.searchTerm)}
  />
   <Movieinput on:submitMovie={event => submitMovie(event.detail.movie)}/>
</div>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  .main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }

  img {
    height: 16rem;
    width: 16rem;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
    line-height: 1.1;
    margin: 2rem auto;
    max-width: 14rem;
  }

  p {
    max-width: 14rem;
    margin: 1rem auto;
    line-height: 1.35;
  }

  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }

    p {
      max-width: none;
    }
  }
</style>
