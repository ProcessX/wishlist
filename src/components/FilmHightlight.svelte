<script>
    import { onMount } from 'svelte';

    const apiKey = `d8aa152441e9d9c755576dd9bbf66733`;
    const apiUrl = `https://api.themoviedb.org/3/movie/550`;

    let movieData = {
        original_title: 'Title',
        overview: 'Overview',
        poster_path: null
    };


    //-------------------------------------------Init---------------------------------

    onMount(async () => {
        getFilmHighlight();
    })

    //-------------------------------------------FUNCTIONS---------------------------------


    /*
    Get film data for display.
    */
    function getFilmHighlight(){
        let film = localStorage.getItem('filmHighlight');

        if(film){
            //Use data if already contained in local storage.
            movieData = JSON.parse(film);
        }
        else{
            //Else, fetch data from API.
            fetchFilmHighlight();
        }
    }


    /*
    Fetch the film's data via the API (The Movie Database)
    */
    function fetchFilmHighlight(){
        let requestUrl = `${apiUrl}?api_key=${apiKey}`;

        fetch(requestUrl)
        .then(
            (response) => {
                return response.json();
            },
            (response) => {
                console.log("Request failed");
            }
        )
        .then(
            (data) => {
                movieData = data;
                //Store film data in local storage for further use.
                storeMovieHighlightData(data);
            }
        )
    }

    /*
    Store the movie's data into the local storage.
    @param [Object] data: The film's data
    */
    function storeMovieHighlightData(data){
        localStorage.setItem('filmHighlight', JSON.stringify(data));
    }


    /*
    Check if local storage already contains data.
    @param [String] address: address to check in local storage.
    */
    function checkLocalStorage(address){
        console.log('Check local storage');
        console.log(localStorage.getItem(address));
    }


</script>


<style>
    /* your styles go here */
</style>



<section class="filmHighlight">
    <img class="movieHightlight__poster" src={`http://image.tmdb.org/t/p/w500${movieData.poster_path}`} alt="movie poster"/>
    <h2 class="filmHightlight__title">{movieData.original_title}</h2>
    <p class="filmHighlight__synopsis">{movieData.overview}</p>
    <button on:click={() => checkLocalStorage('filmHighlight')}>Check local storage</button>
</section>