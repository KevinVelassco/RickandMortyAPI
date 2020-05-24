<template>
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
      message: null
    };
  },
  methods: {
    findAllcharacter() {
      axios
        .get("https://rickandmortyapi.com/api/character/")
        .then(res => {
          this.character = res.data.results;
        })
        .catch(error => {
          this.message = error;
        });
    }
  },
  created() {
    this.findAllcharacter();
  }
};
</script>
