<script>

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
        overflow: hidden;

        .filmSample__poster{
            height: 200px;
            width: 100%;
            max-width: 100%;
            background-color: gray;
            text-indent: 100%;
            overflow: hidden;
        }
    }
</style>


<div class="filmCarousel splide">
    <div class="splide__track">
        <ul class="filmSample__li splide__list">
            {#each filmList as film}
                <li class="filmSample__el splide__slide">
                    <div class="filmSample__poster">Poster</div>
                    <h3 class="filmSample__title">{film.original_title}</h3>
                </li>
            {/each}
        </ul>
    </div>
</div>

