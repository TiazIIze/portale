<template>
  <div class="prodotti">
    <v-data-iterator :items="prodotti" :items-per-page="itemsPerPage">
      <template v-slot:header="{ page, pageCount, prevPage, nextPage }">
        <h1
          class="text-h4 font-weight-bold d-flex justify-space-between mb-4 align-center"
        >
          <div class="text-truncate">Most popular products</div>

          <div class="d-flex align-center">
            <v-btn class="me-8" variant="text" @click="onClickSeeAll">
              <span class="text-decoration-underline text-none">See all</span>
            </v-btn>

            <div class="d-inline-flex">
              <v-btn
                :disabled="page === 1"
                icon="mdi-arrow-left"
                size="small"
                variant="tonal"
                class="me-2"
                @click="prevPage"
              ></v-btn>

              <v-btn
                :disabled="page === pageCount"
                icon="mdi-arrow-right"
                size="small"
                variant="tonal"
                @click="nextPage"
              ></v-btn>
            </div>
          </div>
        </h1>
      </template>

      <template v-slot:default="{ items }">
        <v-row>
          <v-col v-for="(item, i) in items" :key="i" cols="12" sm="5" xl="3">
            <v-sheet border>
              <v-img
                class="product-img"
                hover
                :gradient="`to top right, rgba(255, 255, 255, .1), rgba(${item.raw.color}, .15)`"
                :src="item.raw.thumbnail"
                cover
                height="250"
              >
                <div class="hidden-button-container">
                  <button class="hidden-button" @click="openModal(i)">
                    More photos
                  </button>
                </div>
              </v-img>

              <v-list-item
                lines="two"
                density="comfortable"
                :subtitle="item.raw.description"
              >
                <template v-slot:title>
                  <strong class="text-h6">
                    {{ item.raw.title }}
                  </strong>
                </template>
              </v-list-item>

              <v-table density="compact" class="text-caption">
                <tbody>
                  <tr align="right">
                    <th>Brand:</th>

                    <td>{{ item.raw.brand }}</td>
                  </tr>

                  <tr align="right">
                    <th>Category:</th>

                    <td>{{ item.raw.category }}</td>
                  </tr>

                  <tr align="right">
                    <th>Stock:</th>

                    <td>{{ item.raw.stock }}</td>
                  </tr>

                  <tr align="right">
                    <th>Rating:</th>

                    <td>
                      <div class="text-right">
                        <v-rating
                          v-model="item.raw.rating"
                          half-increments
                          readonly
                          color="rgb(87,227,44)"
                        ></v-rating>
                      </div>
                    </td>
                  </tr>

                  <tr align="right">
                    <th>Price:</th>

                    <td>${{ item.raw.price }}</td>
                  </tr>
                </tbody>
              </v-table>
            </v-sheet>
          </v-col>
        </v-row>
      </template>
    </v-data-iterator>
  </div>
  <div class="carousel">
    <v-dialog v-model="modalModel" max-width="800px" max-height="800px">
      <v-carousel hide-delimiters>
        <v-carousel-item v-for="(item, i) in prodotti" :key="i">
          <v-img :src="item.images[i + 1]" cover></v-img>
        </v-carousel-item>
        <v-btn icon @click="closeModal">
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </v-carousel>
    </v-dialog>
  </div>
</template>
<script>
import products from "../prodotti";
export default {
  data() {
    return {
      itemsPerPage: 6,
      prodotti: [],
      modalModel: false,
      modalItemImages: [],
      modalActiveItem: 0,
    };
  },
  methods: {
    onClickSeeAll() {
      this.itemsPerPage = this.itemsPerPage === 6 ? this.prodotti.length : 6;
    },
    openModal(i) {
      this.modalItemImages = i;
      this.modalModel = true;
    },
    closeModal() {
      this.modalModel = false;
    },
  },
  mounted() {
    this.prodotti = products;
    console.log(products);
  },
};
</script>

<style>
.prodotti {
  /* margin-left: 50px; */
  overflow: hidden; /* Nasconde la barra di scorrimento */
}
.v-table__wrapper {
  overflow: hidden;
}
.v-row {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  flex: 1 1 auto;
  margin: -12px;
}
.v-col-sm-5 {
  flex: 0 0 41.6666666667%;
  max-width: 400px;
}
.mb-4 {
  margin-bottom: 16px !important;
  margin-left: 100px;
  margin-right: 100px;
  color: rgb(59, 131, 59);
}
.v-list-item--two-line .v-list-item-subtitle {
  -webkit-line-clamp: 1;
}
.product-img {
  display: flex;
  align-items: center;
  transition: 0.4s;
}
.product-img:hover {
  cursor: pointer;
  /* opacity: 0.6; */
  transition: 0.4s;
  visibility: visible;
}
.product-img:active {
  opacity: 0.4;
}
.hidden-button-container {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(0, 0, 0, 50%);
  height: 250px;
  width: 100%;
  opacity: 0;
  transition: 0.6s;
}

.hidden-button-container:hover {
  opacity: 1;
  transition: 0.6s;
}
.hidden-button {
  font-size: 25px;
  color: rgb(59, 131, 59);
  background-color: white;
  border-radius: 2px;
  padding-left: 5px;
  padding-right: 5px;
  opacity: 1;
  transition: 0.6s;
}
.hidden-button:active {
  font-size: 27px;
  transition: 0.4s;
}
.carousel {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 500px;
}
</style>
