<template>
    <form @submit.prevent="submit">
        <div class="form-group row mt-8">
            <label for="name" class="col-form-label">Name</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" name="name" id="name" v-model="name">
            </div>
        </div>

        <div class="form-group row">
            <label for="name" class="col-form-label">Permissions</label>
            <div class="col-sm-10">
                <div class="form-check form-check-inline col-3" v-for="permission in permissions" :key="permission.id">
                    <input 
                        type="checkbox" 
                        class="form-check-input" 
                        :value="permission.id" 
                        @change="select(permission.id, $event.target.checked)"
                    >
                    <label class="form-check-label">{{permission.name}}</label>
                </div>
            </div>
        </div>

        <button class="btn btn-outline-secondary" type="submit">Save</button>
    </form>
</template>

<script lang="ts">
import axios from 'axios'
import { onMounted, ref } from 'vue'
import { useRouter } from 'vue-router'

export default {
    name: 'RolesCreate',
    setup() {

        const name = ref('')
        const permissions = ref([])
        const selected = ref([] as number[])

        const router = useRouter()

        onMounted(async () => {
            const response = await axios.get('permissions')
            permissions.value = response.data.data
        })

        const select = (id: number, checked: boolean) => {
            if (checked) {
                selected.value = [...selected.value, id]
                return
            }

            selected.value = selected.value.filter(s => s !== id)
        }

        const submit = async () => {
            await axios.post('roles', {
                name: name.value,
                permissions: selected.value
            })

            await router.push('/roles')
        }

        return {
            name,
            permissions,
            select,
            selected,
            submit
        }
    }
}
</script>