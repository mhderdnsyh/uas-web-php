<template>
  <div class="pengaturan my-3">
    <div class="theme mt-5">
      <h5>Theme</h5>
      <div class="btn-group">
        <a href="#" class="btn btn-secondary active" aria-current="page">Auto</a>
        <a href="#" class="btn btn-light">Light Mode</a>
        <a href="#" class="btn btn-dark">Dark Mode</a>
      </div>
    </div>
    <div class="font mt-4">
      <h5>Fonts</h5>
      <div class="btn-group">
        <a href="#" class="btn btn-secondary active" aria-current="page">Montserrat</a>
        <a href="#" class="btn btn-secondary">Sans Serif</a>
        <a href="#" class="btn btn-secondary">Segoe UI </a>
      </div>
    </div>
    <div class="audio mt-4">
      <h5>Feature</h5>
      <div class="btn-group" role="group" aria-label="Button group with nested dropdown">
        <button id="btnGroupDrop1" type="button" class="btn btn-light dropdown-toggle" data-bs-toggle="dropdown" aria-expanded="false">Gabung jadi Mitra</button>
        <ul class="dropdown-menu" aria-labelledby="btnGroupDrop1">
          <li><a class="dropdown-item" href="#">Mitra Driver</a></li>
          <li><a class="dropdown-item" href="#">Mitra Usaha</a></li>
        </ul>

        <div class="btn-group" role="group">
          <button id="btnGroupDrop1" type="button" class="btn btn-light dropdown-toggle" data-bs-toggle="dropdown" aria-expanded="false">Perusahaan</button>
          <ul class="dropdown-menu" aria-labelledby="btnGroupDrop1">
            <li><a class="dropdown-item" href="#">Tentang</a></li>
            <li><a class="dropdown-item" href="#">Aman</a></li>
            <li><a class="dropdown-item" href="#">Sustainability</a></li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
.pengaturan {
  margin-left: 5rem;
}
h5 {
  color: rgb(71, 70, 70);
}
</style>
