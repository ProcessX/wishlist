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
    .carousel{
        .tns-outer{
            position: relative;

            .tns-control{
                height: 100%;
                width: 100%;
                position: absolute;
                top: 0;
                left: 0;
            }
        }
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
                <FilmSample filmData={film}/>
            </li>
        {/each}
    </ul>
</div>





