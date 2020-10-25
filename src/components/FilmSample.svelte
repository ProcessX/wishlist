<script>
    // your script goes here
    export let filmData;

    let filmPosterURL = `http://image.tmdb.org/t/p/w185/${filmData.poster_path}`;

</script>

<style lang="scss">
    /* your styles go here */

    .filmSample{
        width: inherit;
        max-width: inherit;
    }

    .filmSample__visual{
        width: inherit;
        max-width: inherit;
        height: 200px;
        overflow: hidden;
        background-color: lavender;
        position: relative;
        cursor: pointer;

        .filmSample__poster{
            height: 100%;
            width: 100%;
            text-indent: 100%;
            overflow: hidden;
            background-position: center;
            background-size: cover;
        }

        .filmSample__title{
            position: absolute;
            bottom: 0;
            left: 0;
            margin: 0;
            line-height: 1em;
        }
    }

    .filmSample__info{
        display: flex;
        justify-content: space-between;
    }
</style>

<!-- markup (zero or more items) goes here -->
<div class="filmSample">
    <div class="filmSample__visual">
        <div class="filmSample__poster" style={`background-image: url(${filmPosterURL})`}>Poster</div>
        <h3 class="filmSample__title">{filmData.original_title}</h3>    
    </div>
    <div class="filmSample__info">
        <p class="filmSample__releaseDate">{filmData.release_date.slice(0,4)}</p>
        <p class="filmSample__rating">{filmData.vote_average}</p>
    </div>
</div>