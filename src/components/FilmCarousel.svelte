<script>
    import FilmSample from '../components/FilmSample.svelte';

    export let filmList = [];

    let carousel = {
        children: []
    };


    
    $:{
        if(filmList.length > 0)
            setTimeout(initCarousel, 50)
    }


    function initCarousel(){
        console.log('Init carousel');
        var slider = tns({
            container: carousel,
            items: 3,
            gutter: 10,
            slideBy: "page",
            mouseDrag: true,
            swipeAngle: false,
            speed: 400
        });
    }

</script>


<style lang="scss">
    .carousel__li{
        list-style: none;
        padding: 0;
        margin: 0;
    }

    .carousel__el{
        //width: 120px;
        //max-width: 120px;
    }
</style>

<button on:click={initCarousel}>Carousel</button>
<ul class="carousel__li" bind:this={carousel}>
    {#each filmList as film}
        <li class="carousel__el">
            <FilmSample filmData={film}/>
        </li>
    {/each}
</ul>




