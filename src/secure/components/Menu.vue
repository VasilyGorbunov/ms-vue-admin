<template>
  <nav id="sidebarMenu" class="col-md-3 col-lg-2 d-md-block bg-light sidebar collapse">
    <div class="sidebar-sticky pt-3">
      <ul class="nav flex-column">
        <li class="nav-item">
          <router-link active-class="active" class="nav-link" to="/dashboard">Dashboard</router-link>
        </li>
        <li class="nav-item" v-if="user.canView('users')">
          <router-link active-class="active" class="nav-link" to="/users">Users</router-link>
        </li>
        <li class="nav-item" v-if="user.canView('roles')">
          <router-link active-class="active" class="nav-link" to="/roles">Roles</router-link>
        </li>
        <li class="nav-item" v-if="user.canView('products')">
          <router-link active-class="active" class="nav-link" to="/products">Products</router-link>
        </li>
        <li class="nav-item" v-if="user.canView('orders')">
          <router-link active-class="active" class="nav-link" to="/orders">Orders</router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script lang="ts">
import { computed } from 'vue'
import { useStore } from 'vuex'
  export default {
    name: "Menu",
    setup() {
      const store = useStore()
      const user = computed(() => store.state.User.user)

      return {
        user
      }
    }
  }
</script>