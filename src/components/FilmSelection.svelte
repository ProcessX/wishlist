<script>
    // your script goes here
    import { onMount } from 'svelte';
    import * as queryMult from '../asset/data/RequestQueryMult.json';

    export let title = 'Film selection';

    const listLength = 20;
    const apiKey = `d8aa152441e9d9c755576dd9bbf66733`;
    const apiQuery = `https://api.themoviedb.org/3/discover/movie?api_key=${apiKey}&year=2020`;

    //let selection = [1,2,3];
    let selection = [];


    //-------------------------------------------INIT---------------------------------

    onMount(async () => {
        getSelection();
    });


    //-------------------------------------------FUNCTIONS---------------------------------

    /*
    Get film selection.
    */
    function getSelection(){
        let selectionData = localStorage.getItem(title);

        if(selectionData){
            console.log('Selection already in local storage');
            selection = JSON.parse(selectionData);
        }
        else{
            console.log('Fetch from API');
            fetchSelection();
        }
    }


    /*
    Fetch film selection from API.
    */
    function fetchSelection(){
        fetch(apiQuery)
        .then(
            (response) => {
                return response.json();
            },
            (response) => {
                console.log('Error');
            }
        )
        .then(
            (data) => {
                selection = data.results;
                console.log(selection);
                storeSelection(title, selection);
            }
        );
    }


    /*
    Store film selection in local storage.
    @param [String] address: reference into local storage.
    @param [Object] data: object to store into local storage.
    */
    function storeSelection(address, data){
        localStorage.setItem(address, JSON.stringify(data));
    }


</script>

<style>
    /* your styles go here */
</style>

<!-- markup (zero or more items) goes here -->

<section class="filmSelection">
    <h2 class="filmSelection__title">{title}</h2>

    <ul class="film__li">
        
        {#each selection as film}
            <li class="film__el">
                <h3 class="film__title">{film.original_title}</h3>
            </li>
        {/each}
    </ul>

</section>