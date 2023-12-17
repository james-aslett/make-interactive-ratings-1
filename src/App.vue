<script setup>
import { reactive } from "vue";
import { StarIcon } from "@heroicons/vue/24/solid";
import { items } from "./movies.json";

const movies = reactive(items);

function updateRating(newRating, movie) {
  console.log(`New rating:${newRating}`)
  console.log(`Old rating:${movie.rating}`)
  movie.rating = newRating;
}

</script>

<template>
  <div class="app">
    <div class="movie-list">
      <div class="movie-item" v-for="movie in movies" :key="movie.id">
        <div class="movie-item-image-wrapper">
          <img :src="movie.image" class="movie-item-image" alt="" />
        </div>

        <div class="movie-item-content-wrapper">
          <div class="movie-item-title-wrapper">
            <h3 class="movie-item-title">{{ movie.name }}</h3>
            <div class="movie-item-genres-wrapper">
              <span v-for="genre in movie.genres" :key="`${movie.id}-${genre}`" class="movie-item-genre-tag">{{ genre
              }}</span>
            </div>
          </div>
          <div class="movie-item-description-wrapper">
            <p class="movie-item-description">{{ movie.description }}</p>
          </div>
          <div class="movie-item-rating-wrapper">
            <span class="movie-item-rating-text">
              Rating: ({{ movie.rating }}/5)
            </span>

            <!-- CHALLENGE 2: Create buttons for each rating from 1 to 5 and display a star inside -->
            <!-- CHALLENGE 3: Color the stars based on the movie rating. For example, if the movie rating is 3, color 3 stars yellow and 2 gray -->
            <!-- CHALLENGE 4: Allow the end user to click on any of the 5 buttons to update the movie rating accordingly -->
            <!-- CHALLENGE 5: Disable the button for the currently selected rating to prevent the user from giving the same rating twice -->
            <button @click="updateRating(star, movie)" v-for="(star, index) in 5" :key="`star-${index}`"
              :class="{ 'movie-item-star-icon-yellow': index < movie.rating, 'movie-item-star-icon-gray': index >= movie.rating }"
              :disabled="index + 1 === movie.rating">
              <StarIcon />
            </button>

            <!-- CHALLENGE 1: Remove the display-only stars that we coded in the last challenge -->
            <!-- <StarIcon
              v-for="star in movie.rating"
              :key="`star-${star}`"
              class="movie-item-star-icon"
            /> -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
