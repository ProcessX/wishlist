<script>
    // your script goes here

    export let filmList = [];

</script>


<style lang="scss">
    /* your styles go here */

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


<div class="filmCarousel">
    <ul class="filmSample__li">
        {#each filmList as film}
            <li class="filmSample__el">
                <div class="filmSample__poster">Poster</div>
                <h3 class="filmSample__title">{film.original_title}</h3>
            </li>
        {/each}
    </ul>
</div>

