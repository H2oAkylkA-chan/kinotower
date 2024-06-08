<script setup lang="ts">
import {categories} from "@vueuse/metadata";
import {useCountriesStore} from "~/stores/useCountryStore";


const filmsStore = useFilmsStore();
const categoriesStore = useCategoriesStore();
const countriesStore = useCountriesStore();
const category = ref(null);
const country = ref(null);
const sortBy = ref(null);
const params = ref(null);
filmsStore.fetchFilms();
const reset = () => {
  filmsStore.resetParams()
  category.value = (null);
  country.value = (null);
  sortBy.value = (null);
}
const goto = (page: number) => {
  if (page < 1) {
    filmsStore.params.page = 1;
return;
  } else if (page > filmsStore.totalPages) {
    filmsStore.params.page = filmsStore.totalPages;
   return;

}
filmsStore.params.page = page;
filmsStore.fetchFilms()
}

</script>
<template>


  <div class="row mb-5 mt-4">
    <div class="col d-flex justify-content-around flex-nowrap">
      <div class="text-center position-absolute start-50 translate-middle" style="top: 160px"
           v-if="filmsStore.isLoading">
        <div class="spinner-border" role="status">
          <span class="visually-hidden">Loading...</span>
        </div>
      </div>
      <select v-model="category" @change="filmsStore.addCategoryToParams(category)" class="form-select w-25 me-3"
              aria-label="Default select example">
        <option :value="null">select Genre...</option>
        <option v-for="category in categoriesStore.categories"
                :key="category.id"
                :value="category.id">{{ category.name }}
        </option>
      </select>

      <select v-model="country" @change="filmsStore.addCountryToParams(country)" class="form-select w-25 me-3"
              aria-label="Default select example">
        <option :value="null">select Countries...</option>
        <option v-for="country in countriesStore.countries"
                :key="country.id"
                :value="country.id">
          <template>{{ country.name }}
          </template>
        </option>

      </select>

      <div class="d-flex justify-content-between w-50">
        <select v-model="sortBy" @change="filmsStore.addSortToParams(sortBy)" class="form-select me-3">
          <option value="name" class="option">name</option>
          <option value="year" class="option">year</option>
          <option value="rating" class="option">rating</option>
        </select>
        <button @click="filmsStore.resetParams(),reset()" class="btn btn-dark p-2" style="min-width: 45px">Reset
        </button>

      </div>
    </div>
  </div>

  <div class="row mb-5">
    <div class="col d-flex justify-content-between flex-wrap w-auto" style="gap: 50px">
      <div v-for="film in filmsStore.films" class="card" style="width: 20rem;">
        <img :src="film.link_img" class="card-img-top" style="height: 210px; object-fit: contain; " alt="...">
        <div class="card-body">
          <h5 class="card-title">{{ film.name }}</h5>

          <p class="card-text mb-1">Rating: {{ film.ratingAvg }}</p>
          <p class="card-text mb-3">Duration: {{ film.duration }}</p>
          <p class="card-text">Genres
            <template v-if="!film.categories.length">
              No genres found
            </template>
            <template
                v-for="category in film.categories"
                :key="category.id"
            >
              {{ category.name }},
            </template>
          </p>

          <button class="btn btn-dark w-auto d-block  pe-3 ps-3">
            <a href="#" class="text-white">VIEW</a>
          </button>
        </div>
      </div>
    </div>
  </div>

  <div class="row d-flex justify-content-center w-50 m-auto">
    <nav aria-label="Page navigation example">
      <ul class="pagination">
        <li class="page-item  " :class="filmsStore.params.page == 1 ? 'disabled' : ''">
          <a class="page-link" href="#" aria-label="Previous" @click.prevent="goto(filmsStore.params.page - 1)">
            <span aria-hidden="true">&laquo;</span>
          </a>
        </li>
        <li v-for="page in filmsStore.totalPages" :key="page" :class="filmsStore.params.page == page ? 'active' : ''"><a
            @click.prevent="goto(page)" class="page-link" href="#">{{ page }}</a></li>
        <li class="page-item " :class="filmsStore.params.page == filmsStore.totalPages ? 'disabled' : ''">
          <a class="page-link" href="#" aria-label="Next" @click.prevent="goto(filmsStore.params.page + 1)">
            <span aria-hidden="true">&raquo;</span>
          </a>
        </li>
      </ul>
    </nav>
  </div>
</template>
