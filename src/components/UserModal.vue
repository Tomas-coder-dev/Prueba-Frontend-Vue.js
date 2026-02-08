<template>
  <div class="modal fade show d-block" style="background: rgba(0,0,0,0.5);" tabindex="-1">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">{{ isEditing ? 'Editar Usuario' : 'Agregar Usuario' }}</h5>
          <button type="button" class="btn-close" @click="$emit('close')"></button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="submitForm">
            <div class="mb-3">
              <label class="form-label">Nombre</label>
              <input v-model="form.name" type="text" class="form-control" required />
            </div>
            <div class="mb-3">
              <label class="form-label">Username</label>
              <input v-model="form.username" type="text" class="form-control" required />
            </div>
            <div class="mb-3">
              <label class="form-label">Email</label>
              <input v-model="form.email" type="email" class="form-control" required />
              <div class="form-text">Debe ser un correo válido.</div>
            </div>
            <div class="mb-3">
              <label class="form-label">Teléfono</label>
              <input v-model="form.phone" type="text" class="form-control" required />
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" @click="$emit('close')">Cancelar</button>
              <button type="submit" class="btn btn-primary">{{ isEditing ? 'Actualizar' : 'Guardar' }}</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, computed } from 'vue';

const props = defineProps({ userToEdit: Object });
const emit = defineEmits(['close', 'save']);

const form = ref({ id: null, name: '', username: '', email: '', phone: '' });

const isEditing = computed(() => !!props.userToEdit);

watch(() => props.userToEdit, (newUser) => {
  if (newUser) {
    form.value = { ...newUser };
  } else {
    form.value = { id: null, name: '', username: '', email: '', phone: '' };
  }
}, { immediate: true });

const submitForm = () => emit('save', form.value);
</script>