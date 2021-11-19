<template>
  <div>
    <nav class="d-flex justify-content-between align-items-center">
      <h2 style="color: #f50001">Boolflix</h2>
      <div class="mb-3">
        <input
          type="text"
          class="p-1"
          placeholder="Cerca ..."
          aria-label="Recipient's username"
          aria-describedby="button-addon2"
          v-model="parolaDaCercare"
          @keyup.enter="$emit('mioEvento', parolaDaCercare)"
        />
        <button
          class="btn btn-outline-secondary"
          type="button"
          id="button-addon2"
          @click="printAll()"
        >
          Button
        </button>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      parolaDaCercare: "",
    };
  },
};
</script>

<style>
</style>