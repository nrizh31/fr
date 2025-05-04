<template>
  <div class="empty-state">
    <p>Belum ada kegiatan. Tambahkan kegiatan baru!</p>
  </div>
</template>

<script>
export default {
  name: 'EmptyState'
};
</script>

<style scoped>
.empty-state {
  text-align: center;
  padding: 40px 0;
  color: var(--light-text);
}
</style>
