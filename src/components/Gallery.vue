<template>
  <div class="col-12 col-sm-6 col-lg-4">
    <div class="row character">
      <div class="col-4 content-img">
        <img :src="img" class="img-fluid img" alt="Responsive image" />
      </div>
      <div class="col-8">
        <h5>{{ name }}</h5>
        <h6>{{ status }} - {{ species }}</h6>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Gallery",
  props: ["img", "name", "status", "species"]
};
</script>
<style scoped>
.character {
  border-radius: 5px;
  margin-bottom: 15px;
  -webkit-box-shadow: -1px 0px 14px -6px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: -1px 0px 14px -6px rgba(0, 0, 0, 0.75);
  box-shadow: -1px 0px 14px -6px rgba(0, 0, 0, 0.75);
}
.content-img {
  padding-right: 0px !important;
  padding-left: 0px !important;
}
.img {
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
}
</style>
