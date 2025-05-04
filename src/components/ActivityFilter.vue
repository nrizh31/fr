<template>
    <div class="filter-options">
      <div class="filter-toggle">
        <input 
          type="checkbox" 
          id="filter-toggle" 
          :checked="showOnlyIncomplete"
          @change="$emit('update:showOnlyIncomplete', $event.target.checked)"
          class="checkbox"
        >
        <label for="filter-toggle">Tampilkan hanya kegiatan yang belum selesai</label>
      </div>
      <div class="activity-count">
        {{ activeCount }} kegiatan belum selesai
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      showOnlyIncomplete: {
        type: Boolean,
        default: false
      },
      activeCount: {
        type: Number,
        default: 0
      }
    },
    emits: ['update:showOnlyIncomplete']
  };
  </script>
  
  <style scoped>
  .filter-options {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
    align-items: center;
  }
  
  .filter-toggle {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  
  .filter-toggle label {
    font-size: 16px;
    color: var(--light-text);
  }
  
  .activity-count {
    font-size: 16px;
    color: var(--light-text);
  }
  
  .checkbox {
    width: 22px;
    height: 22px;
    accent-color: var(--success-color);
    cursor: pointer;
  }
  </style>