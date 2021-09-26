<template>
  <div>
    <div class="row text-center mt-5 ms-5 me-5">
      <div class="col">
        <h2>Mata Kuliah</h2>
      </div>
      <div class="col">
        <h2>Hari Tenggat</h2>
      </div>
      <div class="col">
        <h2>Aksi</h2>
      </div>
    </div>
    <div v-for="hasi in hasil" v-bind:key="hasi.id">
      <IsiTugas v-bind:id="hasi.id" v-bind:matakuliah="hasi.matakuliah" v-bind:haritenggat="haritenggat" v-bind:hasi="hasi" v-bind:hasil="hasil" v-on:delete-hasil="$emit('delete-hasil', hasi.id)" />
    </div>
  </div>
</template>

<script>
import IsiTugas from "./IsiTugas.vue";
export default {
  name: "Hasil",
  components: {
    IsiTugas,
  },
  props: ["hasil"],
};
</script>

<style scoped></style>
