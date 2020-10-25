<script>
    import FilmSample from '../components/FilmSample.svelte';

    export let filmList = [];

    $:{
        if(filmList.length > 0)
            initCarousel();
    }

    function initCarousel(){
        console.log('Init carousel');

    }

</script>


<style lang="scss">
    .filmSample__li{
        list-style: none;
        padding: 0;
        margin: 0;
    }

    .filmSample__el{
        width: 120px;
        max-width: 120px;
    }
</style>


<div class="filmCarousel splide">
    <div class="splide__track">
        <ul class="filmSample__li splide__list">
            {#each filmList as film}
                <li class="filmSample__el splide__slide">
                    <FilmSample filmData={film}/>
                </li>
            {/each}
        </ul>
    </div>
</div>

