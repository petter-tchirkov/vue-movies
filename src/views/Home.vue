<template>
  <div class="home">
    <div class="feature">
      <!-- <router-link to="/movie/tt0409591">
        <div class="feature-card">
          <img
            src="http://avatars.mds.yandex.net/get-kinopoisk-image/1704946/e63beb56-0433-4bbf-ae70-5d85a5ed8945/600x900"
            alt="naruto"
            class="feature-img"
          />
          <div class="feature-detail">
            <h3>Naruto</h3>
            <p>
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Laborum
              voluptatem delectus fugiat perspiciatis aperiam maxime, minus ut
              quia cum totam, eum alias consequatur impedit voluptate, repellat
              animi eius quod excepturi accusamus asperiores aliquam saepe quis
              quaerat veniam. Nulla hic ipsa veniam odio enim ipsum omnis
              blanditiis, eaque quibusdam animi sint?
            </p>
          </div>
        </div>
      </router-link> -->
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input
        type="text"
        placeholder="What are you looking for?"
        v-model="search"
      />
      <input type="submit" value="Search" />
    </form>
    <div class="movie-list">
      <div v-for="movie in movies" :key="movie.imdbID" class="product">
        <router-link :to="'/movie/' + movie.imdbID" class="product-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="" />
            <div class="product-type">{{ movie.Type }}</div>
          </div>
          <div class="product-detail">
            <p class="product-year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import env from "@/env.js";
export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    };

    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>

<style lang="scss">
.home {
  .feature {
    position: relative;
    &-img {
      display: block;
      width: 100%;
      height: 400px;
      object-fit: cover;
    }
    &-card,
    &-detail {
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
    }
    &-detail {
      background-color: rgba(0, 0, 0, 0.6);
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      z-index: 1;
      padding: 10px;
      h3 {
        color: #fff;
        margin-bottom: 16px;
      }
      p {
        color: #fff;
      }
    }
  }
}
.search-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 16px;
  input {
    display: block;
    appearance: none;
    border: none;
    outline: none;
    background: none;
    &[type="text"] {
      width: 100%;
      color: #fff;
      background-color: #496583;
      font-size: 20px;
      padding: 10px 16px;
      border-radius: 8px;
      margin-bottom: 15px;
      transition: 0.4s;
      &::placeholder {
        color: #f3f3f3;
      }
      &:focus {
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.2);
      }
    }
    &[type="submit"] {
      width: 100%;
      max-width: 300px;
      background-color: #42b883;
      padding: 16px;
      border-radius: 8px;
      font-size: 20px;
      color: #fff;
      text-transform: uppercase;
      transition: 0.4s;
      &:active {
        background-color: #3b8070;
      }
    }
  }
}
.movie-list {
  display: flex;
  flex-wrap: wrap;
  margin: 0 8px;
  .product {
    max-width: 50%;
    flex: 1 1 50%;
    padding: 16px 8px;
    &-link {
      display: flex;
      flex-direction: column;
      height: 100%;
    }
    &-image {
      position: relative;
      display: block;
      img {
        display: block;
        width: 100%;
        height: 275px;
        object-fit: cover;
      }
    }
    &-type {
      position: absolute;
      padding: 8px 16px;
      background-color: #42b883;
      color: #fff;
      bottom: 16px;
      left: 0px;
      text-transform: capitalize;
    }
    &-detail {
      background-color: #496583;
      padding: 16px 8px;
      flex: 1 1 50%;
      border-radius: 0 0 8px 8px;
    }
    &-year {
      color: #aaa;
      font-size: 14px;
    }
    h3 {
      color: #fff;
      font-weight: 600;
      font-size: 18px;
    }
  }
}
</style>
