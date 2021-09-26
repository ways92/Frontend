<template>
  <div>
    <div class="container mt-5">
      <h1 class="text-center">
        Daftar Tugas Kuliah
      </h1>

      <button type="button" class="btn btn-secondary" data-bs-toggle="modal" data-bs-target="#exampleModal">
        + Tugas
      </button>

      <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">Tugas Kuliah</h5>
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <form @submit="Tambah">
              <div class="modal-body">
                <div class="mb-3">
                  <label for="exampleFormControlInput1" class="form-label">Mata Kuliah</label>
                  <input type="text" class="form-control" v-model="matakuliah" name="matakuliah" id="" placeholder="Isi Mata Kuliah" />
                </div>
                <div class="mb-3">
                  <label for="exampleFormControlInput1" class="form-label">Hari Tenggat</label>
                  <input type="text" class="form-control" v-model="haritenggat" name="haritenggat" id="" placeholder="Isi Hari Tenggat" />
                </div>
              </div>
              <div class="modal-footer">
                <button class="btn btn-secondary" data-bs-dismiss="modal">Tambah</button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Tambah",
  data() {
    return {
      matakuliah: "",
      haritenggat: "",
    };
  },
  methods: {
    Tambah(e) {
      e.preventDefault();
      const newTugas = {
        id: Date.now(),
        matakuliah: this.matakuliah,
        haritenggat: this.haritenggat,
      };

      this.$emit("tambah-tugas", newTugas);
      this.matakuliah = "";
      this.haritenggat = "";
    },
  },
};
</script>

<style scoped></style>
