<script setup>
import { ref, onMounted } from 'vue';
import { userService } from './services/api';
import UserModal from './components/UserModal.vue';

const users = ref([]);
const loading = ref(true);
const showModal = ref(false);
const selectedUser = ref(null);

onMounted(async () => {
  try {
    users.value = await userService.getUsers();
  } catch (error) {
    console.error(error);
  } finally {
    loading.value = false;
  }
});

const openModal = (user = null) => {
  selectedUser.value = user;
  showModal.value = true;
};

const handleSaveUser = (formData) => {
  if (formData.id) {
    const index = users.value.findIndex(u => u.id === formData.id);
    if (index !== -1) {
      users.value[index] = { ...formData };
    }
  } else {
    const maxId = users.value.length > 0 ? Math.max(...users.value.map(u => u.id)) : 0;
    users.value.push({ ...formData, id: maxId + 1 });
  }
  showModal.value = false;
};

const deleteUser = (id) => {
  if (confirm("¿Está seguro de eliminar este usuario?")) {
    users.value = users.value.filter(u => u.id !== id);
  }
};
</script>

<template>
  <div class="container mt-5">
    <div class="d-flex justify-content-between align-items-center mb-4">
      <h2>Gestión de Usuarios</h2>
      <button class="btn btn-success" @click="openModal(null)">+ Agregar Usuario</button>
    </div>

    <div v-if="loading" class="text-center py-5">
      <div class="spinner-border text-primary" role="status"></div>
      <p class="mt-2">Cargando datos...</p>
    </div>

    <div v-else class="table-responsive shadow-sm p-3 bg-body rounded">
      <table class="table table-hover align-middle">
        <thead class="table-dark">
          <tr>
            <th>ID</th><th>Nombre</th><th>Username</th><th>Email</th><th>Teléfono</th><th class="text-end">Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td>{{ user.id }}</td>
            <td>{{ user.name }}</td>
            <td>{{ user.username }}</td>
            <td>{{ user.email }}</td>
            <td>{{ user.phone }}</td>
            <td class="text-end">
              <button class="btn btn-sm btn-outline-primary me-2" @click="openModal(user)">Editar</button>
              <button class="btn btn-sm btn-outline-danger" @click="deleteUser(user.id)">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <UserModal v-if="showModal" :userToEdit="selectedUser" @close="showModal = false" @save="handleSaveUser" />
  </div>
</template>

<style>
body { background-color: #f8f9fa; }
</style>