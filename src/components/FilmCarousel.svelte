<script>
    import FilmSample from '../components/FilmSample.svelte';

    export let filmList = [];

    let carousel;
    let filmLoaded = false;

    $:{
        if(filmList.length > 0){
            setTimeout(initCarousel, 50)
        }
    }

    function initCarousel(){
        var slider = tns({
            container: carousel,
            items: 3,
            gutter: 10,
            slideBy: "page",
            mouseDrag: true,
            swipeAngle: false,
            speed: 400
        });

        filmLoaded = true;
    }

</script>


<style lang="scss">

    :global(.tns-outer){
        position: relative;
    }

    :global(.tns-controls){
        height: 100%;
        width: 100%;
        position: absolute;
        display: flex;
        justify-content: space-between;
        z-index: 100;
        pointer-events: none;
    }

    :global(.tns-controls button){
        pointer-events: all;
    }

    :global(.tns-nav){
        display: none;
    }

    .filmSample__li{
        list-style: none;
        padding: 0;
        margin: 0;
    }

</style>


<div class="carousel">
    <ul class="filmSample__li" bind:this={carousel}>
        {#each filmList as film}
            <li class="filmSample__el">
                <FilmSample filmData={film} filmLoaded={filmLoaded}/>
            </li>
        {/each}
    </ul>
</div>





