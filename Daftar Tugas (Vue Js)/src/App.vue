<template>
  <div class="container mt-5">
    <h2 class="text-center">Daftar Tugas Kuliah</h2>
    <button class="btn btn-dark mb-3 mt-3" data-bs-toggle="modal" data-bs-target="#exampleModal">TAMBAH</button>
    <!-- Modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">TAMBAH TUGAS</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <form @submit.prevent="save2">
            <div class="modal-body">
              <div class="mb-3">
                <input type="hidden" v-model="form2.id" />
                <label for="exampleInputMK1" class="form-label">Mata Kuliah</label>
                <input type="text" v-model="form2.mk" name="matakuliah" class="form-control" />
              </div>
              <div class="mb-3">
                <label for="exampleInputTG1" class="form-label">Tenggat</label>
                <input type="text" v-model="form2.tg" name="tenggat" class="form-control" />
              </div>
            </div>
            <div class="modal-footer">
              <button type="submit" name="button" class="btn btn-dark">SAVE</button>
            </div>
          </form>
        </div>
      </div>
    </div>
    <!-- end of modal -->

    <table class="table table-dark table-striped">
      <thead>
        <tr>
          <th scope="col">NO</th>
          <th scope="col" class="text-center">Mata Kuliah</th>
          <th scope="col" class="text-center">Hari Tenggat</th>
          <th scope="col" class="text-center">Aksi</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(tugas, index) in tugass" :key="tugas.id">
          <th scope="row">{{ index + 1 }}</th>
          <td>{{ tugas.mk }}</td>
          <td>{{ tugas.tg }}</td>
          <td class="text-center">
            <button v-on:click="edit2(tugas)" class="btn btn-warning" data-bs-toggle="modal" data-bs-target="#exampleEdit">EDIT</button> ||
            <button v-on:click="hapus2(tugas)" class="btn btn-danger">DELETE</button>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- modal edit -->
    <div class="modal fade" id="exampleEdit" tabindex="-1" aria-labelledby="exampleModalLabel1">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel1">EDIT TUGAS</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <form @submit.prevent="save2">
            <div class="modal-body">
              <div class="mb-3">
                <input type="hidden" v-model="form2.id" />
                <label for="exampleInputMK1" class="form-label">Mata Kuliah</label>
                <input type="text" v-model="form2.mk" name="matakuliah" class="form-control" />
              </div>
              <div class="mb-3">
                <label for="exampleInputTG1" class="form-label">Tenggat</label>
                <input type="text" v-model="form2.tg" name="tenggat" class="form-control" />
              </div>
            </div>
            <div class="modal-footer">
              <button type="submit" v-on:click="update2(form2)" name="button" class="btn btn-success">UPDATE</button>
            </div>
          </form>
        </div>
      </div>
    </div>
    <!-- end of modal edit -->
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      form2: {
        id: "",
        mk: "",
        tg: "",
      },
      tugass: [],
    };
  },
  methods: {
    load2() {
      axios
        .get("http://localhost:3000/tugass")
        .then((ress) => {
          this.tugass = ress.data;
        })
        .catch(() => {
          alert("error load data");
        });
    },
    save2() {
      axios
        .post("http://localhost:3000/tugass", this.form2)
        .then(() => {
          this.load2();
          this.form2.mk = "";
          this.form2.tg = "";
        })
        .catch(() => {});
    },
    hapus2(tugas) {
      axios
        .delete("http://localhost:3000/tugass/" + tugas.id)
        .then(() => {
          this.load2();
          this.form2.mk = "";
          this.form2.tg = "";
        })
        .catch(() => {
          alert("delete error");
        });
    },
    edit2(tugas) {
      this.updateSubmit2 = true;
      this.form2.id = tugas.id;
      this.form2.mk = tugas.mk;
      this.form2.tg = tugas.tg;
    },
    update2(form2) {
      axios
        .put("http://localhost:3000/tugass/" + form2.id, {
          mk: this.form2.mk,
          tg: this.form2.tg,
        })
        .then(() => {
          this.load2();
          this.form2.mk = "";
          this.form2.tg = "";
        })
        .catch(() => {
          alert("update error");
        });
    },
    //----------------------------------------------------------------------------------------------
  },
  mounted() {
    //buat  menampilkan data
    this.load2();
  },
};
</script>

<style></style>
