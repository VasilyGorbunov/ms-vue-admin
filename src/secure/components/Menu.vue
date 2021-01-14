<template>
  <nav id="sidebarMenu" class="col-md-3 col-lg-2 d-md-block bg-light sidebar collapse">
    <div class="sidebar-sticky pt-3">
      <ul class="nav flex-column">
        
          <router-link class="nav-link active" to="/">
            Dashboard
          </router-link>
          <router-link class="nav-link active" to="/users">
            Users
          </router-link>
        
      </ul>
    </div>
  </nav>
</template>

<script>
  export default {
    name: "Menu"
  }
</script>