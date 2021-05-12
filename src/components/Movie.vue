<template>
  <div>
    <div class="row m-4">
      <div class="col-8 mx-auto">
        <div class="card">
          <h4 class="m-3">Añadir Pelicula</h4>

          <form class="p-3" v-on:submit.prevent="submit()">
            <div class="row mb-3">
              <div class="col-3">
                <label for="title" class="form-label">Title</label>
              </div>
              <div class="col-9">
                <input
                  type="text"
                  class="form-control"
                  id="title"
                  required
                  v-model="title"
                />
              </div>
            </div>
            <div class="row mb-3">
              <div class="col-3">
                <label for="year" class="form-label">Year</label>
              </div>
              <div class="col-9">
                <input
                  type="number"
                  class="form-control"
                  id="year"
                  required
                  v-model="year"
                />
              </div>
            </div>
            <div class="row mb-3">
              <div class="col-3">
                <label for="genre" class="form-label">Genre</label>
              </div>
              <div class="col-9">
                <input
                  type="text"
                  class="form-control"
                  id="genre"
                  required
                  v-model="genre"
                />
              </div>
            </div>
            <div class="row justify-content-end">
              <button type="submit" class="btn btn-primary col-3 me-3">
                Add
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col-8 mx-auto">
        <table class="table table-striped ">
          <thead>
            <tr>
              <th scope="col" style="cursor:pointer;" @click="orderMovies(1)">
                Title
              </th>
              <th scope="col" style="cursor:pointer;" @click="orderMovies(2)">
                Year
              </th>
              <th scope="col" style="cursor:pointer;" @click="orderMovies(3)">
                Genres
              </th>
              <th scope="col">
                Delete
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(movie, index) in movies" :key="index">
              <th scope="row">{{ movie.title }}</th>
              <td>{{ movie.year }}</td>
              <td>{{ movie.genre }}</td>
              <td>
                <button
                  class="btn btn-outline-danger"
                  @click="deleteMovie(index)"
                >
                  X
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Movie',
  data() {
    return {
      movies: [],
      title: '',
      year: null,
      genre: '',
    };
  },
  methods: {
    orderMovies: function(option) {
      if (option === 1) {
        this.movies = this.movies.sort(function(movieA, movieB) {
          return movieA.title > movieB.title;
        });
      } else if (option === 2) {
        this.movies = this.movies.sort(function(movieA, movieB) {
          return movieA.year - movieB.year;
        });
      } else {
        this.movies = this.movies.sort(function(movieA, movieB) {
          return movieA.genre > movieB.genre;
        });
      }
    },
    submit: function() {
      let movie = {
        title: this.title,
        year: this.year,
        genre: this.genre,
      };
      this.movies.push(movie);
      this.title = '';
      this.year = null;
      this.genre = '';
    },
    deleteMovie: function(index) {
      this.movies.splice(index, 1);
    },
  },
};
</script>

<style></style>
