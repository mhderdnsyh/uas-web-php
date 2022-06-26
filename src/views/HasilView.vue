<template>
  <div class="hasil">
    <div id="appppp">
      <div class="container-fluid">
        <div class="row bg-dark">
          <div class="col-lg-12">
            <!-- <p class="text-center text-light display-4 pt-2" style="font-size: 25px">Hasil Pemesanan</p> -->
          </div>
        </div>
      </div>
      <div class="container">
        <div class="row mt-3">
          <div class="col-lg-6">
            <h3 class="text-dark">Data Pemesanan</h3>
          </div>
          <div class="col-lg-6">
            <button class="btn btn-dark float-right" @click="showAddModal = true"><i class="fas fa-users"></i>&nbsp;&nbsp;Add New Pemesanan</button>
          </div>
        </div>
        <hr class="bg-dark" />
        <div class="alert alert-danger" v-if="errorMsg">{{ errorMsg }}</div>
        <div class="alert alert-success" v-if="successMsg">
          {{ successMsg }}
        </div>
        <!-- display hasil -->
        <div class="row">
          <div class="col-lg-12">
            <table class="table table-bordered table-striped">
              <thead>
                <tr class="text-center bg-dark text-light">
                  <th>Id Pemesanan</th>
                  <th>Id Pelanggan</th>
                  <th>Nama Pelanggan</th>
                  <th>Id Food</th>
                  <th>Id Drink</th>
                  <th>Edit</th>
                  <th>Delete</th>
                </tr>
              </thead>
              <tbody>
                <tr class="text-center" v-for="hasil in hasils" :key="hasil">
                  <td>{{ hasil.id_pemesanan }}</td>
                  <td>{{ hasil.id_pelanggan }}</td>
                  <td>{{ hasil.nama_pelanggan }}</td>
                  <td>{{ hasil.id_food }}</td>
                  <td>{{ hasil.id_drink }}</td>

                  <td>
                    <a
                      href="#"
                      class="btn btn-success"
                      @click="
                        showEditModal = true;
                        selectHasil(hasil);
                      "
                      ><i class="glyphicon glyphicon-edit">Ubah</i></a
                    >
                  </td>
                  <td>
                    <a
                      href="#"
                      class="btn btn-danger"
                      @click="
                        showDeleteModal = true;
                        selectHasil(hasil);
                      "
                      ><i class="glyphicon glyphicon-trash">Hapus</i></a
                    >
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <!-- add new hasil -->
      <div id="overlay" v-if="showAddModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Add New Hasil</h5>
              <button type="button" class="close" @click="showAddModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <form action="#" method="post">
                <div class="form-group mb-2">
                  <input type="number" name="id_pemesanan" class="form-control form-control-lg" placeholder="Id Pemesanan" v-model="newHasils.id_pemesanan" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="id_pelanggan" class="form-control form-control-lg" placeholder="Id Pelanggan" v-model="newHasils.id_pelanggan" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="nama_pelanggan" class="form-control form-control-lg" placeholder="Nama Pelanggan" v-model="newHasils.nama_pelanggan" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="id_food" class="form-control form-control-lg" placeholder="Id Food" v-model="newHasils.id_food" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="id_drink" class="form-control form-control-lg" placeholder="Id Drink" v-model="newHasils.id_drink" />
                </div>

                <div class="form-group">
                  <button
                    class="btn btn-dark btn-block btn-lg mt-3"
                    style="color: white"
                    @click="
                      showAddModal = false;
                      addHasils();
                      clearMsg();
                    "
                  >
                    Add Hasil
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>

      <!-- Edit hasil -->
      <div id="overlay" v-if="showEditModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Edit Hasil</h5>
              <button type="button" class="close" @click="showEditModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <form action="#" method="post">
                <div class="form-group mb-2">
                  <input type="number" name="id_pemesanan" class="form-control form-control-lg" v-model="currentHasil.id_pemesanan" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="id_pelanggan" class="form-control form-control-lg" v-model="currentHasil.id_pelanggan" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="nama_pelanggan" class="form-control form-control-lg" v-model="currentHasil.nama_pelanggan" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="id_food" class="form-control form-control-lg" v-model="currentHasil.id_food" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="id_drink" class="form-control form-control-lg" v-model="currentHasil.id_drink" />
                </div>

                <div class="form-group">
                  <button
                    class="btn btn-dark btn-block btn-lg mt-3"
                    style="color: white"
                    @click="
                      showEditModal = false;
                      updateHasil();
                      clearMsg();
                    "
                  >
                    Perbarui Hasil
                    <!-- Update Hasil -->
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>

      <!-- Delete hasil -->
      <div id="overlay" v-if="showDeleteModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Delete Hasil</h5>
              <button type="button" class="close" @click="showDeleteModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <h4>apakah kamu setuju menghapus data pemesanan ini?</h4>
              <h5 class="confirm mt-3">kamu menghapus pemesanan {{ currentHasil.id_pemesanan }}</h5>
              <hr />
              <button
                class="btn btn-danger btn-lg mt-3"
                @click="
                  showDeleteModal = false;
                  deleteHasil();
                  clearMsg();
                "
              >
                Yes
              </button>
              &nbsp;&nbsp;&nbsp;&nbsp;
              <button class="btn btn-success btn-lg mt-3" @click="showDeleteModal = false">No</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";

export default {
  name: "HasilView",

  data: () => {
    return {
      showAddModal: false,
      showEditModal: false,
      showDeleteModal: false,
      errorMsg: "",
      successMsg: "",
      hasils: [],
      newHasils: {
        id_pemesanan: "",
        id_pelanggan: "",
        nama_pelanggan: "",
        id_food: "",
        id_drink: "",
      },
      currentHasil: {},
    };
  },
  mounted: function () {
    this.getAllHasils();
  },
  methods: {
    getAllHasils() {
      axios.get("https://uaslaverpool.000webhostapp.com/hasils.php?action=read").then((res) => {
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          // console.warn(res.data.users);
          this.hasils = res.data.hasils;
        }
      });
    },
    addHasils() {
      var formData = this.toFormData(this.newHasils);
      axios.post("https://uaslaverpool.000webhostapp.com/hasils.php?action=create", formData).then((res) => {
        this.newHasils = {
          id_pemesanan: "",
          id_pelanggan: "",
          nama_pelanggan: "",
          id_food: "",
          id_drink: "",
        };
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllHasils();
        }
      });
    },
    updateHasil() {
      var formData = this.toFormData(this.currentHasil);
      axios.post("https://uaslaverpool.000webhostapp.com/hasils.php?action=update", formData).then((res) => {
        this.currentHasil = {};
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllHasils();
        }
      });
    },
    deleteHasil() {
      var formData = this.toFormData(this.currentHasil);
      axios.post("https://uaslaverpool.000webhostapp.com/hasils.php?action=delete", formData).then((res) => {
        this.currentHasil = {};
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllHasils();
        }
      });
    },
    toFormData(obj) {
      var fd = new FormData();
      for (var i in obj) {
        fd.append(i, obj[i]);
      }
      return fd;
    },
    selectHasil(hasil) {
      this.currentHasil = hasil;
    },
    clearMsg() {
      this.errorMsg = "";
      this.successMsg = "";
    },
  },
};
</script>
<style>
.container {
  text-align: center;
}
.container .btn-info {
  color: #ffff;
}
#overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgb(0, 0, 0, 0.6);
}
</style>
