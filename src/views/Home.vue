<template>
  <div>
    <div class="row sticky-top" id="header">
      <div class="col-12">
        <div class="col-12">
          <p class="text-center title">R&M Personajes</p>
        </div>
        <div class="row justify-content-center">
          <nav aria-label="Page navigation example">
            <ul class="pagination">
              <li
                class="page-item"
                style="cursor:pointer"
                :class="disabledPagination.disabledPrevious"
              >
                <a
                  class="page-link"
                  @click="changePage(page - 1)"
                  aria-label="Anterior"
                >
                  <span aria-hidden="true">&laquo;</span>
                </a>
              </li>
              <li class="page-item active" aria-current="page">
                <a class="page-link">
                  {{ page }}
                  <span class="sr-only">(current)</span>
                </a>
              </li>
              <li
                class="page-item"
                style="cursor:pointer"
                :class="disabledPagination.disabledNext"
              >
                <a
                  class="page-link"
                  @click="changePage(page + 1)"
                  aria-label="Siguiente"
                >
                  <span aria-hidden="true">&raquo;</span>
                </a>
              </li>
            </ul>
          </nav>
        </div>
      </div>
    </div>
    <div class="row mt-3">
      <Gallery
        v-for="charact of character"
        :key="charact.id"
        :name="charact.name"
        :img="charact.image"
        :status="charact.status"
        :species="charact.species"
      ></Gallery>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Gallery from "@/components/Gallery";
export default {
  name: "Home",
  components: {
    Gallery
  },
  data() {
    return {
      character: null,
      message: null,
      page: 1,
      pages: 1
    };
  },
  computed: {
    disabledPagination() {
      return {
        disabledPrevious: this.page === 1 ? "disabled" : "",
        disabledNext: this.page >= this.pages ? "disabled" : ""
      };
    }
  },
  methods: {
    findAllcharacter() {
      const params = {
        page: this.page
      };

      axios
        .get("https://rickandmortyapi.com/api/character/", { params })
        .then(res => {
          this.character = res.data.results;
          this.pages = res.data.info.pages;
        })
        .catch(error => {
          this.message = error;
        });
    },
    changePage(page) {
      console.log("change " + page);

      this.page = page <= 0 || page > this.pages ? this.page : page;
      this.findAllcharacter();
    }
  },
  created() {
    this.findAllcharacter();
  }
};
</script>
<style scoped>
#header {
  background-color: #ffffff;
  font-weight: 600;
  padding: 5px;
  -webkit-box-shadow: -1px 0px 14px -6px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: -1px 0px 14px -6px rgba(0, 0, 0, 0.75);
  box-shadow: -1px 0px 14px -6px rgba(0, 0, 0, 0.75);
}
.title {
  font-size: 30px;
}
</style>
