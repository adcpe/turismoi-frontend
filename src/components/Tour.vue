<template>
  <div class="tours">
    <section v-for="(el, i) in data.data.data" :key="i" class="card">
      <div class="card__image">
        <img :src="el.attributes.principal_photo" :alt="el.attributes.name" />
      </div>
      <div class="card__info">
        <div class="info-left">
          <h1>{{ el.attributes.name }}</h1>
          <p>{{ el.attributes.avg_hours }} horas</p>
        </div>
        <div class="info-right">
          <p>{{ el.attributes.country_iso }}</p>
          <p>$ {{ el.attributes.dolar_price }}</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios';

const url =
  'https://api.turismoi.com/api/tours?page%5Bpage%5D=1&page%5Bper_page%5D=10';

const config = {
  headers: {
    'Accept-Search-Filters': 'yes',
    Accept: 'application/vnd.api+json',
    'Content-Type': 'application/vnd.api+json',
    Authorization: `Token ${process.env.VUE_APP_APIKEY}`,
  },
};

export default {
  methods: {
    getAllTours: () => {
      return axios(url, config);
    },
  },
  data() {
    return {
      data: {},
    };
  },
  created() {
    this.getAllTours().then((res) => (this.data = res));
  },
};
</script>

<style lang="scss">
.tours {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
}

.card {
  display: grid;
  height: 300px;
  grid-template-columns: 40% 1fr;
  border: 1px black solid;

  .card__image {
    margin: 0;
    overflow: hidden;

    img {
      display: block;
      margin-top: -10%;
      margin-left: -40%;
    }
  }
}
</style>
