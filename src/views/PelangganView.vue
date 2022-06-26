<template>
  <div class="pelanggan">
    <div id="apppp">
      <div class="container-fluid">
        <div class="row bg-dark">
          <div class="col-lg-12">
            <!-- <p class="text-center text-light display-4 pt-2" style="font-size: 25px">Data Pelanggan</p> -->
          </div>
        </div>
      </div>
      <div class="container">
        <div class="row mt-3">
          <div class="col-lg-6">
            <h3 class="text-dark">Data pelanggan Laverpool</h3>
          </div>
          <div class="col-lg-6">
            <button class="btn btn-dark float-right" @click="showAddModal = true"><i class="fas fa-users"></i>&nbsp;&nbsp;Add New Pelanggan</button>
          </div>
        </div>
        <hr class="bg-dark" />
        <div class="alert alert-danger" v-if="errorMsg">{{ errorMsg }}</div>
        <div class="alert alert-success" v-if="successMsg">
          {{ successMsg }}
        </div>
        <!-- display data -->
        <div class="row">
          <div class="col-lg-12">
            <table class="table table-bordered table-striped">
              <thead>
                <tr class="text-center bg-dark text-light">
                  <th>Id Pelanggan</th>
                  <th>Nama</th>
                  <th>Email</th>
                  <th>Alamat</th>
                  <th>Jenis Kelamin</th>
                  <th>No Hp</th>
                  <th>Edit</th>
                  <th>Delete</th>
                </tr>
              </thead>
              <tbody>
                <tr class="text-center" v-for="pelanggan in pelanggans" :key="pelanggan">
                  <td>{{ pelanggan.id_pelanggan }}</td>
                  <td>{{ pelanggan.nama }}</td>
                  <td>{{ pelanggan.email }}</td>
                  <td>{{ pelanggan.alamat }}</td>
                  <td>{{ pelanggan.jenis_kelamin }}</td>
                  <td>{{ pelanggan.no_hp }}</td>
                  <td>
                    <a
                      href="#"
                      class="btn btn-success"
                      @click="
                        showEditModal = true;
                        selectPelanggan(pelanggan);
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
                        selectPelanggan(pelanggan);
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

      <!-- add new pelanggan -->
      <div id="overlay" v-if="showAddModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Add New Pelanggan</h5>
              <button type="button" class="close" @click="showAddModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <form action="#" method="post">
                <div class="form-group mb-2">
                  <input type="number" name="id_pelanggan" class="form-control form-control-lg" placeholder="Id Pelanggan" v-model="newPelanggans.id_pelanggan" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="nama" class="form-control form-control-lg" placeholder="Nama" v-model="newPelanggans.nama" />
                </div>
                <div class="form-group mb-2">
                  <input type="email" name="email" class="form-control form-control-lg" placeholder="Email" v-model="newPelanggans.email" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="alamat" class="form-control form-control-lg" placeholder="Alamat" v-model="newPelanggans.alamat" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="jenis_kelamin" class="form-control form-control-lg" placeholder="Jenis Kelamin" v-model="newPelanggans.jenis_kelamin" />
                </div>
                <div class="form-group mb-2">
                  <input type="tel" name="no_hp" class="form-control form-control-lg" placeholder="No Hp" v-model="newPelanggans.no_hp" />
                </div>

                <div class="form-group">
                  <button
                    class="btn btn-dark btn-block btn-lg mt-3"
                    style="color: white"
                    @click="
                      showAddModal = false;
                      addPelanggans();
                      clearMsg();
                    "
                  >
                    Add Pelanggan
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>

      <!-- Edit pelanggan -->
      <div id="overlay" v-if="showEditModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Edit Pelanggan</h5>
              <button type="button" class="close" @click="showEditModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <form action="#" method="post">
                <div class="form-group mb-2">
                  <input type="number" name="id_pelanggan" class="form-control form-control-lg" v-model="currentPelanggan.id_pelanggan" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="nama" class="form-control form-control-lg" v-model="currentPelanggan.nama" />
                </div>
                <div class="form-group mb-2">
                  <input type="email" name="email" class="form-control form-control-lg" v-model="currentPelanggan.email" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="alamat" class="form-control form-control-lg" v-model="currentPelanggan.alamat" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="jenis_kelamin" class="form-control form-control-lg" v-model="currentPelanggan.jenis_kelamin" />
                </div>
                <div class="form-group mb-2">
                  <input type="tel" name="no_hp" class="form-control form-control-lg" v-model="currentPelanggan.no_hp" />
                </div>

                <div class="form-group">
                  <button
                    class="btn btn-dark btn-block btn-lg mt-3"
                    style="color: white"
                    @click="
                      showEditModal = false;
                      updatePelanggan();
                      clearMsg();
                    "
                  >
                    Update Pelanggan
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>

      <!-- Delete pelanggan -->
      <div id="overlay" v-if="showDeleteModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Delete Pelanggan</h5>
              <button type="button" class="close" @click="showDeleteModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <h4>apakah kamu setuju menghapus data pelanggan ini?</h4>
              <h5 class="confirm mt-3">kamu menghapus data pelanggan {{ currentPelanggan.nama }}</h5>
              <hr />
              <button
                class="btn btn-danger btn-lg mt-3"
                @click="
                  showDeleteModal = false;
                  deletePelanggan();
                  clearMsg();
                "
              >
                Setuju
              </button>
              &nbsp;&nbsp;&nbsp;&nbsp;
              <button class="btn btn-success btn-lg mt-3" @click="showDeleteModal = false">Tidak</button>
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
  name: "PelangganView",

  data: () => {
    return {
      showAddModal: false,
      showEditModal: false,
      showDeleteModal: false,
      errorMsg: "",
      successMsg: "",
      pelanggans: [],
      newPelanggans: {
        id_pelanggan: "",
        nama: "",
        email: "",
        alamat: "",
        jenis_kelamin: "",
        no_hp: "",
      },
      currentPelanggan: {},
    };
  },
  mounted: function () {
    this.getAllPelanggans();
  },
  methods: {
    getAllPelanggans() {
      axios.get("https://uaslaverpool.000webhostapp.com/pelanggans.php?action=read").then((res) => {
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          // console.warn(res.data.users);
          this.pelanggans = res.data.pelanggans;
        }
      });
    },
    addPelanggans() {
      var formData = this.toFormData(this.newPelanggans);
      axios.post("https://uaslaverpool.000webhostapp.com/pelanggans.php?action=create", formData).then((res) => {
        this.newPelanggans = {
          id_pelanggan: "",
          nama: "",
          email: "",
          alamat: "",
          jenis_kelamin: "",
          no_hp: "",
        };
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllPelanggans();
        }
      });
    },
    updatePelanggan() {
      var formData = this.toFormData(this.currentPelanggan);
      axios.post("https://uaslaverpool.000webhostapp.com/pelanggans.php?action=update", formData).then((res) => {
        this.currentPelanggan = {};
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllPelanggans();
        }
      });
    },
    deletePelanggan() {
      var formData = this.toFormData(this.currentPelanggan);
      axios.post("https://uaslaverpool.000webhostapp.com/pelanggans.php?action=delete", formData).then((res) => {
        this.currentPelanggan = {};
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllPelanggans();
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
    selectPelanggan(pelanggan) {
      this.currentPelanggan = pelanggan;
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
