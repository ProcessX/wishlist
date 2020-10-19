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


    function getFilmHighlight(){
        let film = localStorage.getItem('filmHighlight');
        //console.log(film);

        if(film){
            movieData = JSON.parse(film);
        }
        else{
            fetchFilmHighlight();
        }
    }


    /*
    Fetch the film's data via the API (The Movie Database)
    */
    function fetchFilmHighlight(){

        let requestUrl = `${apiUrl}?api_key=${apiKey}`;
        console.log(requestUrl);
        console.log("Get film hightlight");


        //movieData = localStorage.getItem('movieHighlight');
        //console.log(movieData);

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
                console.log(data);
                storeMovieHighlightData(data);
            }
        )
    }


    function storeMovieHighlightData(data){
        console.log('Store movie highlight');
        localStorage.setItem('filmHighlight', JSON.stringify(data));
    }


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