<template>
  <div class="tours">
    <section v-for="(el, i) in data.data.data" :key="i" class="card">
      <div class="card__image">
        <img :src="el.attributes.principal_photo" :alt="el.attributes.name" />
      </div>
      <div class="card__info">
        <div class="left">
          <h1>{{ el.attributes.name }}</h1>
          <p>
            {{
              el.attributes.avg_hours >= 12
                ? 'Full Day (1 día)'
                : `${el.attributes.avg_hours} horas`
            }}
          </p>
        </div>
        <div class="right">
          <p class="flag">{{ getFlag(el.attributes.country_iso) }}</p>
          <p>
            Desde:
            <br />
            ${{ Math.floor(el.attributes.dolar_price) }}
          </p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios';
import flag from 'country-code-emoji';

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
    getFlag: (code) => {
      return flag(code);
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
  margin: 1rem auto;
}

.card {
  display: grid;
  height: 300px;
  grid-template-columns: 40% 1fr;
  border: 1px black solid;
  border-top-left-radius: 1rem;
  border-bottom-left-radius: 1rem;

  h1 {
    font-size: 0.95rem;
  }

  > div {
    display: flex;
    align-content: center;
  }

  .left {
    text-align: left;
  }

  .card__image {
    margin: 0;
    overflow: hidden;

    img {
      display: block;
      margin-top: -10%;
      margin-left: -40%;
      border-top-left-radius: 1rem;
      border-bottom-left-radius: 1rem;
    }
  }

  .card__info {
    display: grid;
    grid-template-columns: 1fr 1fr;
    width: 80%;
    margin: 0 auto;
  }
}

.flag {
  font-size: 1.5rem;
}
</style>
