<template>
  <div class="drink">
    <div id="appp">
      <div class="container-fluid">
        <div class="row bg-dark">
          <div class="col-lg-12">
            <!-- <p class="text-center text-light display-4 pt-2" style="font-size: 25px">Data Drink</p> -->
          </div>
        </div>
      </div>
      <div class="container">
        <div class="row mt-3">
          <div class="col-lg-6">
            <h3 class="text-dark">Data drink Laverpool</h3>
          </div>
          <div class="col-lg-6">
            <button class="btn btn-light float-right" @click="showAddModal = true"><i class="fas fa-users"></i>&nbsp;&nbsp;Add Drink</button>
          </div>
        </div>
        <hr class="bg-info" />
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
                  <th>Id Drink</th>
                  <th>Nama Drink</th>
                  <th>Harga Drink</th>
                  <th>Stok Drink</th>
                  <th>Jumlah Pesanan</th>
                  <th>Deskripsi Drink</th>
                  <th>Edit</th>
                  <th>Delete</th>
                </tr>
              </thead>
              <tbody>
                <tr class="text-center" v-for="drink in drinks" :key="drink">
                  <td>{{ drink.id_drink }}</td>
                  <td>{{ drink.nama_drink }}</td>
                  <td>{{ drink.harga_drink }}</td>
                  <td>{{ drink.stok_drink }}</td>
                  <td>{{ drink.jml_pesanan }}</td>
                  <td>{{ drink.desc_drink }}</td>
                  <td>
                    <a
                      href="#"
                      class="btn btn-success"
                      @click="
                        showEditModal = true;
                        selectDrink(drink);
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
                        selectDrink(drink);
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

      <!-- add new drink -->
      <div id="overlay" v-if="showAddModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Add Drink</h5>
              <button type="button" class="close" @click="showAddModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <form action="#" method="post">
                <div class="form-group mb-2">
                  <input type="number" name="id_drink" class="form-control form-control-lg" placeholder="Id Drink" v-model="newDrinks.id_drink" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="nama_drink" class="form-control form-control-lg" placeholder="Nama Drink" v-model="newDrinks.nama_drink" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="harga_drink" class="form-control form-control-lg" placeholder="Harga Drink" v-model="newDrinks.harga_drink" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="stok_drink" class="form-control form-control-lg" placeholder="Stok Drink" v-model="newDrinks.stok_drink" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="jml_pesanan" class="form-control form-control-lg" placeholder="Jumlah Pesanan" v-model="newDrinks.jml_pesanan" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="desc_drink" class="form-control form-control-lg" placeholder="Deskripsi Drink" v-model="newDrinks.desc_drink" />
                </div>
                <div class="form-group">
                  <button
                    class="btn btn-dark btn-block btn-lg mt-3"
                    style="color: white"
                    @click="
                      showAddModal = false;
                      addDrinks();
                      clearMsg();
                    "
                  >
                    Add Drink
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>

      <!-- Edit drink -->
      <div id="overlay" v-if="showEditModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Edit Drink</h5>
              <button type="button" class="close" @click="showEditModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <form action="#" method="post">
                <div class="form-group mb-2">
                  <input type="number" name="id_drink" class="form-control form-control-lg" v-model="currentDrink.id_drink" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="nama_drink" class="form-control form-control-lg" v-model="currentDrink.nama_drink" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="harga_drink" class="form-control form-control-lg" v-model="currentDrink.harga_drink" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="stok_drink" class="form-control form-control-lg" v-model="currentDrink.stok_drink" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="jml_pesanan" class="form-control form-control-lg" v-model="currentDrink.jml_pesanan" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="desc_drink" class="form-control form-control-lg" v-model="currentDrink.desc_drink" />
                </div>

                <div class="form-group">
                  <button
                    class="btn btn-dark btn-block btn-lg mt-3"
                    style="color: white"
                    @click="
                      showEditModal = false;
                      updateDrink();
                      clearMsg();
                    "
                  >
                    Update Drink
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>

      <!-- Delete drink -->
      <div id="overlay" v-if="showDeleteModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Delete Drink</h5>
              <button type="button" class="close" @click="showDeleteModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <h4>apakah kamu setuju menghapus minuman ini?</h4>
              <h5>kamu menghapus minuman {{ currentDrink.nama_drink }}</h5>
              <hr />
              <button
                class="btn btn-danger btn-lg"
                @click="
                  showDeleteModal = false;
                  deleteDrink();
                  clearMsg();
                "
              >
                Setuju
              </button>
              &nbsp;&nbsp;&nbsp;&nbsp;
              <button class="btn btn-success btn-lg" @click="showDeleteModal = false">Tidak</button>
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
  name: "DrinkView",

  data: () => {
    return {
      showAddModal: false,
      showEditModal: false,
      showDeleteModal: false,
      errorMsg: "",
      successMsg: "",
      drinks: [],
      newDrinks: {
        id_drink: "",
        nama_drink: "",
        harga_drink: "",
        stok_drink: "",
        jml_pesanan: "",
        desc_drink: "",
      },
      currentDrink: {},
    };
  },
  mounted: function () {
    this.getAllDrinks();
  },
  methods: {
    getAllDrinks() {
      axios.get("https://uaslaverpool.000webhostapp.com/drinks.php?action=read").then((res) => {
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          // console.warn(res.data.users);
          this.drinks = res.data.drinks;
        }
      });
    },
    addDrinks() {
      var formData = this.toFormData(this.newDrinks);
      axios.post("https://uaslaverpool.000webhostapp.com/drinks.php?action=create", formData).then((res) => {
        this.newDrinks = {
          id_drink: "",
          nama_drink: "",
          harga_drink: "",
          stok_drink: "",
          jml_pesanan: "",
          desc_drink: "",
        };
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllDrinks();
        }
      });
    },
    updateDrink() {
      var formData = this.toFormData(this.currentDrink);
      axios.post("https://uaslaverpool.000webhostapp.com/drinks.php?action=update", formData).then((res) => {
        this.currentDrink = {};
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllDrinks();
        }
      });
    },
    deleteDrink() {
      var formData = this.toFormData(this.currentDrink);
      axios.post("https://uaslaverpool.000webhostapp.com/drinks.php?action=delete", formData).then((res) => {
        this.currentDrink = {};
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllDrinks();
        }
      });
    },
    toFormData(objj) {
      var fdd = new FormData();
      for (var ii in objj) {
        fdd.append(ii, objj[ii]);
      }
      return fdd;
    },
    selectDrink(drink) {
      this.currentDrink = drink;
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
