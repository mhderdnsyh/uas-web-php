<template>
  <div class="food">
    <div id="app">
      <div class="container-fluid">
        <div class="row bg-dark">
          <div class="col-lg-12">
            <!-- <p class="text-center text-light display-4 pt-2" style="font-size: 25px">Data Food</p> -->
          </div>
        </div>
      </div>
      <div class="container">
        <div class="row mt-3">
          <div class="col-lg-6">
            <h3 class="text-dark">Data food Laverpool</h3>
          </div>
          <div class="col-lg-6">
            <button class="btn btn-light float-right" @click="showAddModal = true"><i class="fas fa-users"></i>&nbsp;&nbsp;Add Food</button>
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
                  <th>Id Food</th>
                  <th>Nama Food</th>
                  <th>Harga Food</th>
                  <th>Stok Food</th>
                  <th>Jumlah Pesanan</th>
                  <th>Deskripsi Food</th>
                  <th>Edit</th>
                  <th>Delete</th>
                </tr>
              </thead>
              <tbody>
                <tr class="text-center" v-for="food in foods" :key="food">
                  <td>{{ food.id_food }}</td>
                  <td>{{ food.nama_food }}</td>
                  <td>{{ food.harga_food }}</td>
                  <td>{{ food.stok_food }}</td>
                  <td>{{ food.jml_pesanan }}</td>
                  <td>{{ food.desc_food }}</td>
                  <td>
                    <a
                      href="#"
                      class="btn btn-success"
                      @click="
                        showEditModal = true;
                        selectFood(food);
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
                        selectFood(food);
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

      <!-- add new food -->
      <div id="overlay" v-if="showAddModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Add Food</h5>
              <button type="button" class="close" @click="showAddModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <form action="#" method="post">
                <div class="form-group mb-2">
                  <input type="number" name="id_food" class="form-control form-control-lg" placeholder="Id Food" v-model="newFoods.id_food" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="nama_food" class="form-control form-control-lg" placeholder="Nama Food" v-model="newFoods.nama_food" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="harga_food" class="form-control form-control-lg" placeholder="Harga Food" v-model="newFoods.harga_food" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="stok_food" class="form-control form-control-lg" placeholder="Stok Food" v-model="newFoods.stok_food" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="jml_pesanan" class="form-control form-control-lg" placeholder="Jumlah Pesanan" v-model="newFoods.jml_pesanan" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="desc_food" class="form-control form-control-lg" placeholder="Deskripsi Food" v-model="newFoods.desc_food" />
                </div>
                <div class="form-group">
                  <button
                    class="btn btn-dark btn-block btn-lg mt-3"
                    style="color: white"
                    @click="
                      showAddModal = false;
                      addFoods();
                      clearMsg();
                    "
                  >
                    Add Food
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>

      <!-- Edit food -->
      <div id="overlay" v-if="showEditModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Edit Food</h5>
              <button type="button" class="close" @click="showEditModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <form action="#" method="post">
                <div class="form-group mb-2">
                  <input type="number" name="id_food" class="form-control form-control-lg" v-model="currentFood.id_food" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="nama_food" class="form-control form-control-lg" v-model="currentFood.nama_food" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="harga_food" class="form-control form-control-lg" v-model="currentFood.harga_food" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="stok_food" class="form-control form-control-lg" v-model="currentFood.stok_food" />
                </div>
                <div class="form-group mb-2">
                  <input type="number" name="jml_pesanan" class="form-control form-control-lg" v-model="currentFood.jml_pesanan" />
                </div>
                <div class="form-group mb-2">
                  <input type="text" name="desc_food" class="form-control form-control-lg" v-model="currentFood.desc_food" />
                </div>

                <div class="form-group">
                  <button
                    class="btn btn-dark btn-block btn-lg mt-3"
                    style="color: white"
                    @click="
                      showEditModal = false;
                      updateFood();
                      clearMsg();
                    "
                  >
                    Update Food
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>

      <!-- Delete food -->
      <div id="overlay" v-if="showDeleteModal">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Delete Food</h5>
              <button type="button" class="close" @click="showDeleteModal = false">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body p-4">
              <h4>apakah kamu setuju untuk menghapus data food ini?</h4>
              <h5>kamu sedang menghapus {{ currentFood.nama_food }}</h5>
              <hr />
              <button
                class="btn btn-danger btn-lg"
                @click="
                  showDeleteModal = false;
                  deleteFood();
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
  name: "FoodView",

  data: () => {
    return {
      showAddModal: false,
      showEditModal: false,
      showDeleteModal: false,
      errorMsg: "",
      successMsg: "",
      foods: [],
      newFoods: {
        id_food: "",
        nama_food: "",
        harga_food: "",
        stok_food: "",
        jml_pesanan: "",
        desc_food: "",
      },
      currentFood: {},
    };
  },
  mounted: function () {
    this.getAllFoods();
  },
  methods: {
    getAllFoods() {
      axios.get("https://uaslaverpool.000webhostapp.com/foods.php?action=read").then((res) => {
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          // console.warn(res.data.users);
          this.foods = res.data.foods;
        }
      });
    },
    addFoods() {
      var formData = this.toFormData(this.newFoods);
      axios.post("https://uaslaverpool.000webhostapp.com/foods.php?action=create", formData).then((res) => {
        this.newFoods = {
          id_food: "",
          nama_food: "",
          harga_food: "",
          stok_food: "",
          jml_pesanan: "",
          desc_food: "",
        };
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllFoods();
        }
      });
    },
    updateFood() {
      var formData = this.toFormData(this.currentFood);
      axios.post("https://uaslaverpool.000webhostapp.com/foods.php?action=update", formData).then((res) => {
        this.currentFood = {};
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllFoods();
        }
      });
    },
    deleteFood() {
      var formData = this.toFormData(this.currentFood);
      axios.post("https://uaslaverpool.000webhostapp.com/foods.php?action=delete", formData).then((res) => {
        this.currentFood = {};
        if (res.data.error) {
          this.errorMsg = res.data.message;
        } else {
          this.successMsg = res.data.message;
          this.getAllFoods();
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
    selectFood(food) {
      this.currentFood = food;
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
