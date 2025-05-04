<template>
    <ul class="activity-list">
      <transition-group name="transition-group">
        <li 
          v-for="activity in activities" 
          :key="activity.id"
          :class="['activity-item', { 'completed': activity.completed }]"
        >
          <div class="activity-info">
            <input 
              type="checkbox" 
              :checked="activity.completed"
              @change="$emit('toggle-complete', activity.id)"
              class="checkbox"
            >
            <span class="activity-text">{{ activity.text }}</span>
          </div>
          <div class="activity-actions">
            <button 
              class="action-btn btn-danger" 
              @click="$emit('delete-activity', activity.id)"
            >
              Hapus
            </button>
          </div>
        </li>
      </transition-group>
    </ul>
  </template>
  
  <script>
  export default {
    props: {
      activities: {
        type: Array,
        default: () => []
      }
    },
    emits: ['toggle-complete', 'delete-activity']
  };
  </script>
  
  <style scoped>
  .activity-list {
    list-style: none;
    margin-top: 20px;
  }
  
  .activity-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    border-bottom: 1px solid #eee;
    transition: all 0.3s ease;
  }
  
  .activity-item:hover {
    background-color: #f9f9f9;
  }
  
  .activity-info {
    display: flex;
    align-items: center;
    gap: 12px;
    flex: 1;
  }
  
  .activity-text {
    font-size: 16px;
    transition: all 0.3s ease;
  }
  
  .completed .activity-text {
    text-decoration: line-through;
    color: var(--light-text);
    font-style: italic;
  }
  
  .activity-actions {
    display: flex;
    gap: 10px;
  }
  
  .action-btn {
    padding: 8px 12px;
    font-size: 14px;
  }
  
  .btn-danger {
    background-color: var(--danger-color);
  }
  
  .btn-danger:hover {
    background-color: #bd2130;
  }
  
  .checkbox {
    width: 22px;
    height: 22px;
    accent-color: var(--success-color);
    cursor: pointer;
  }
  </style>