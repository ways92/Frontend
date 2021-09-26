<template>
  <div>
    <div class="container mt-5">
      <!-- <table class="table table-dark table-striped">
        <thead>
          <tr>
            <th scope="col" class="text-center">Mata Kuliah</th>
            <th scope="col" class="text-center">Hari Tenggat</th>
            <th scope="col" class="text-center">Aksi</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>{{ hasi.matakuliah }}</td>
            <td>{{ hasi.haritenggat }}</td>
            <td class="text-center">
              <button class="fas fa-edit btn btn-light me-3" @click="editHasil" data-bs-toggle="modal" data-bs-target="#exampleModal1"></button>
              <button class="far fa-trash-alt btn btn-danger" @click="$emit('delete-hasil', hasi.id)"></button>
            </td>
          </tr>
        </tbody>
      </table> -->

      <div class="row mt-5">
        <div class="col">
          <div class="text-start">
            <h5>
              {{ hasi.matakuliah }}
            </h5>
          </div>
        </div>
        <div class="col">
          <div class="text-center">
            <h5>
              {{ hasi.haritenggat }}
            </h5>
          </div>
        </div>
        <div class="col">
          <div class="d-flex justify-content-end">
            <div>
              <button class="fas fa-edit btn btn-warning me-3" @click="editHasil(item)" data-bs-toggle="modal" data-bs-target="#exampleModal1"></button>
            </div>
            <div>
              <button class="far fa-trash-alt btn btn-danger" @click="$emit('delete-hasil', hasi.id)"></button>
            </div>
          </div>
        </div>
      </div>

      <div class="modal fade" id="exampleModal1" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">Tugas Kuliah</h5>
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <form @submit="editHasil">
              <div class="modal-body">
                <div class="mb-3">
                  <label for="exampleFormControlInput1" class="form-label ">Mata Kuliah</label>
                  <input type="text" class="form-control" v-model="editMK" name="matakuliah" />
                </div>
                <div class="mb-3">
                  <label for="exampleFormControlInput1" class="form-label ">Hari Tenggat</label>
                  <input type="text" class="form-control" v-model="editHT" name="haritenggat" />
                </div>
              </div>
              <div class="modal-footer">
                <button class="btn btn-secondary" data-bs-dismiss="modal" type="submit">Simpan</button>
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
  name: "IsiTugas",
  props: ["hasil", "hasi", "matakuliah", "haritenggat", "id"],
  methods: {
    editHasil(e) {
      e.preventDefault();
      console.log(this.id);
      console.log(this.matakuliah);
      console.log(this.haritenggat);
      this.hasil.filter((hasi) => {
        if (this.hasi.id == hasi.id) {
          hasi.matakuliah = this.editMK;
          hasi.haritenggat = this.editHT;
        }
      });
    },
  },
  data() {
    return {
      editMK: "",
      editHT: "",
    };
  },
};
</script>
