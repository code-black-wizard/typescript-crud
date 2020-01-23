<template>
  <div>
    <div class="container-fluid mb-5">
      <div class="row justify-content-around align-items-center bg-dark">
        <div class="col-md-4 navbar-brand text-light">
          Test for AW
        </div>
        <div class="col-md-4 d-flex justify-content-end">
          <nav class="navbar navbar-expand-lg">
            <ul class="navbar-nav">
              <li class="nav-item">
                <router-link to="/" exact class="nav-link">Users</router-link>
              </li>
              <li class="nav-item">
                <router-link to="/courses" class="nav-link">Courses</router-link>
              </li>
            </ul>
          </nav>  
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: 'TheNavBar'
});
</script>

<style scoped>
.nav-link {
  color: #ffffff;
}

.active {
  color: #17a2b8;
}
</style>
