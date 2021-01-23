<template>
    <div class="container">
        <div v-show="loaded" class="loader"></div>
        <div class="column is-one-third" v-for="content in contents.results" :key="content.id">
            <router-link :to="{name: 'MoviesNowPlaying' , params:{id: content.id}}">
            <div class="card">
                <div class="card-image">
                    <figure class="image">
                        <img :src="imageUrl + content.backdrop_path" alt="Image">
                    </figure>
                </div>
                <div class="card-content">
                    <div class="media">
                        <div class="media-left">
                            <figure class="image is-25x25">
                                <img id="poster-image" :src="imageUrl + content.poster_path" alt="Image">
                            </figure>
                        </div>
                        <div class="media-content">
                            <p id="movie-title" class="title is-4 no-padding">{{content.title}}</p>
                            <p><span class="title is-6"><i class="fas fa-star">{{" " + content.vote_average}}</i></span></p>
                            <p class="subtitle is-6"><i  class="fas fa-calendar-alt">{{" " + content.release_date}}</i></p>
                        </div>
                    </div>
                    <div id="overviews" class="content">
                        <p>{{ content.overview}}</p>
                        <div class="background-icon"><span class="icon-twitter"></span></div>
                    </div>
                </div>
            </div>
            </router-link>
        </div>

    </div>

</template>

<script>
export default {
}
</script>
