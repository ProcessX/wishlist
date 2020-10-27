<script>

    import {onMount} from 'svelte';

    import FilmSample from '../components/FilmSample.svelte';

    export let filmList = [];

    let carousel;
    let filmPosterRatio = 1.5;
    let filmLoaded = false;
    let resBreakpoints = [
        {
            res: 480,
            items: 2
        },
        {
            res: 800,
            items: 3
        }
    ];


    $:{
        if(filmList.length > 0){
            setTimeout(initCarousel, 50)
        }
    }

    onMount( () => {
        setCarouselHeight();
    });

    //window.onresize = setCarouselHeight;


    /**
     * Initiate carousel (also with responsive breakpoints)
     */
    function initCarousel(){
        let responsiveData = getCarouselResponsiveData();

        var slider = tns({
            container: carousel,
            items: 1,
            gutter: 0,
            slideBy: "page",
            mouseDrag: true,
            swipeAngle: false,
            speed: 400,
            responsive: responsiveData
        });

        filmLoaded = true;
    }


    /**
     * Return an object containing the data for making the carousel responsive (with breakpoint and item number).
     */
    function getCarouselResponsiveData(){
        let responsiveData = new Object();

        resBreakpoints.forEach((breakpoint) => {
            responsiveData[breakpoint.res] = {
                items: breakpoint.items
            }
        });

        return responsiveData;
    }


    /**
     * Set carousel's height to match the film sample's ratio.
     */
    function setCarouselHeight(){
        let filmSampleWidth = carousel.offsetWidth;
        let filmNbr = getFilmNbr(filmSampleWidth);
        console.log(filmNbr);
        filmSampleWidth /= filmNbr;

        carousel.style.height = `${filmSampleWidth * filmPosterRatio}px`;
    }


    /**
     * Return the nbr of film displayed in on page of the carousel.
     * @param1 carouselWidth: current width of the carousel
    */
   function getFilmNbr(carouselWidth){
        let filmNbr = 1;
        if(carouselWidth < resBreakpoints[0].res){
            return filmNbr;
        }
        else{
            for(let i = 0; i < (resBreakpoints.length - 1); i++){
                if((resBreakpoints[i].res < carouselWidth) && (carouselWidth < resBreakpoints[i + 1].res)){
                    filmNbr = resBreakpoints[i].items;
                    return filmNbr;
                }
            }
        }
        return resBreakpoints[resBreakpoints.length - 1].items;
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

    .carousel{
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





