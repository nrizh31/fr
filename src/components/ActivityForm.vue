<template>
  <div class="form-group">
    <input 
      type="text" 
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      placeholder="Masukkan kegiatan baru..."
      @keyup.enter="$emit('add-activity')"
    >
    <button @click="$emit('add-activity')">Tambah Kegiatan</button>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: String,
      default: ''
    }
  },
  emits: ['update:modelValue', 'add-activity']
};
</script>

<style scoped>
.form-group {
  margin-bottom: 20px;
  display: flex;
  gap: 10px;
}

input {
  flex: 1;
  padding: 12px 15px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-size: 16px;
}
</style>