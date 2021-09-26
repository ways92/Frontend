<template>
  <div>
    <Tambah v-on:tambah-tugas="Tambah" />
    <Hasil v-on:delete-hasil="deleteHasil" v-bind:hasil="hasil" />
  </div>
</template>

<script>
import Tambah from "./components/Tambah.vue";
import Hasil from "./components/Hasil.vue";

export default {
  name: "App",
  components: {
    Tambah,
    Hasil,
  },
  data() {
    return {
      hasil: [
        {
          id: "1",
          matakuliah: "Matematika",
          haritenggat: "Selasa",
        },
        {
          id: "2",
          matakuliah: "Biologi",
          haritenggat: "Senin",
        },
        {
          id: "3",
          matakuliah: "Kimia",
          haritenggat: "Kamis",
        },
        {
          id: "4",
          matakuliah: "Fisika",
          haritenggat: "Rabu",
        },
      ],
    };
  },
  methods: {
    Tambah(newTugas) {
      this.hasil = [...this.hasil, newTugas];
    },
    deleteHasil(id) {
      this.hasil = this.hasil.filter((hasi) => hasi.id !== id);
    },
  },
};
</script>

<style></style>
