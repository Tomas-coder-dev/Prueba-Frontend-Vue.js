# 📋 Sistema de Gestión de Usuarios (CRUD) - Vue 3

Este proyecto es una **Single Page Application (SPA)** desarrollada con **Vue.js 3** y **Vite**, diseñada para gestionar un listado de usuarios consumiendo una API pública y simulando la persistencia de datos de manera local.

## 🚀 Tecnologías Utilizadas

* **Framework:** Vue 3 (Composition API & `<script setup>`)
* **Entorno de Desarrollo:** Vite
* **Cliente HTTP:** Axios
* **UI/Estilos:** Bootstrap 5
* **Lenguaje:** JavaScript (ES6+)

---

## ✅ Requerimientos Cumplidos

El proyecto cumple con la totalidad de los puntos solicitados en el ejercicio técnico:

### 1. Listado de Usuarios (READ)
* Consumo de la API pública `jsonplaceholder.typicode.com/users`.
* Implementación de **Indicador de Carga (Loading)** para mejorar la UX durante la petición asíncrona.
* Visualización de datos en una tabla responsiva.

### 2. Agregar Usuario (CREATE)
* Uso de **Modal** reutilizable para la captura de datos.
* **Lógica Local:** Los nuevos usuarios se agregan al array en memoria (sin enviarlos a la API).
* **Generación de ID:** Se calcula automáticamente el siguiente ID disponible (`Max ID + 1`) para mantener la secuencia lógica.

### 3. Editar Usuario (UPDATE)
* Reutilización del componente Modal adaptado para edición.
* **Reactividad:** Clonado de datos al abrir el formulario para evitar mutaciones directas en la tabla antes de guardar.
* Actualización instantánea del estado local mediante búsqueda por índice (`findIndex`).

### 4. Eliminar Usuario (DELETE)
* Implementación de **Confirmación de Seguridad** nativa (`confirm()`) antes de borrar.
* Actualización reactiva de la lista mediante filtrado de arrays (`filter`).

### 5. Validaciones y Calidad
* **Validación de Email:** Uso de atributos nativos de HTML5 (`type="email"` y `required`) para una validación eficiente y ligera.
* **Arquitectura Limpia:** Separación de responsabilidades (Servicios, Componentes y Vistas).

---

## 📂 Estructura del Proyecto

Se aplicó el principio de **Separación de Responsabilidades** para garantizar la escalabilidad y el orden del código:

```text
src/
├── components/
│   └── UserModal.vue   # Componente "Dumb": Solo maneja el formulario UI y valida.
├── services/
│   └── api.js          # Capa de Servicio: Centraliza la comunicación con Axios.
├── App.vue             # Componente "Smart": Gestiona el estado y la lógica CRUD.
└── main.js             # Configuración global (Bootstrap).
