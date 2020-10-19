<script>
    import { onMount } from 'svelte';

    const apiKey = `d8aa152441e9d9c755576dd9bbf66733`;
    const apiUrl = `https://api.themoviedb.org/3/movie/550`;

    let movieData = {
        title: 'Title',
        overview: 'Overview'
    };


    //-------------------------------------------Init---------------------------------
/*
    onMount(async () => {
        getFilmHighlight();
    })
*/
    //-------------------------------------------FUNCTIONS---------------------------------

    function getFilmHighlight(){

        let requestUrl = `${apiUrl}?api_key=${apiKey}`;
        console.log(requestUrl);
        console.log("Get film hightlight");

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
                movieData.title = data.original_title;
                movieData.overview = data.overview;
                console.log(data);
            }
        )
    }
</script>


<style>
    /* your styles go here */
</style>



<section class="filmHighlight">
    <h2 class="filmHightlight__title">{movieData.title}</h2>
    <p class="filmHighlight__synopsis">{movieData.overview}</p>
    <button on:click={getFilmHighlight}>Request API</button>
</section>