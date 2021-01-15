<template>
    <div class="table-responsive">
    <table class="table table-striped table-sm">
      <thead>
      <tr>
        <th>#</th>
        <th>Name</th>
        <th>Action</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="role in roles" :key="role.id">
        <td>{{ role.id }}</td>
        <td>{{ role.name }}</td>
        <td>
            <div class="btn-group mr-2">
                <router-link :to="`/roles/${role.id}/edit`" class="btn btn-sm btn-outline-secondary">Edit</router-link>
                <a href="javascript:void(0)" class="btn btn-sm btn-outline-secondary" @click="del(role.id)">Delete</a>
            </div>
        </td>
      </tr>
      </tbody>
    </table>
    </div>
</template>

<script lang="ts">
import { onMounted, ref } from 'vue'
import axios from 'axios'
import { Entity } from '@/interfaces/entity'

export default {
    name: 'Roles',
    setup() {
        const roles = ref([])

        const del = async (id: number) => {
            if(confirm('Are you sure you want to delete this record?')) {
                await axios.delete(`roles/${id}`)
                roles.value = roles.value.filter((e: Entity) => e.id !== id)
            }
        }

        onMounted(async () => {
            const response = await axios.get('roles')
            roles.value = response.data.data
        })

        return {
            roles,
            del
        }
    }
}
</script>