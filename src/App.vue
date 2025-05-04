<template>
  <div class="container">
    <h1>Aplikasi Pendaftaran Kegiatan</h1>
    
    <ActivityForm 
      v-model="newActivity"
      @add-activity="addActivity"
    />
    
    <ActivityFilter
      v-model:show-only-incomplete="showOnlyIncomplete"
      :active-count="activeActivityCount"
    />
    
    <ActivityList
      :activities="filteredActivities"
      @toggle-complete="toggleComplete"
      @delete-activity="deleteActivity"
    />
    
    <EmptyState v-if="filteredActivities.length === 0" />
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import ActivityForm from './components/ActivityForm.vue';
import ActivityFilter from './components/ActivityFilter.vue';
import ActivityList from './components/ActivityList.vue';
import EmptyState from './components/EmpetyState.vue'; // perhatikan penamaan

export default {
  components: {
    ActivityForm,
    ActivityFilter,
    ActivityList,
    EmptyState
  },
  setup() {
    const activities = ref([
      { id: 1, text: 'Membuat aplikasi Vue.js', completed: false },
      { id: 2, text: 'Belajar Vite.js', completed: false },
      { id: 3, text: 'Memahami Composition API', completed: true }
    ]);
    const newActivity = ref('');
    const showOnlyIncomplete = ref(false);
    
    const filteredActivities = computed(() => {
      return showOnlyIncomplete.value
        ? activities.value.filter(activity => !activity.completed)
        : activities.value;
    });
    
    const activeActivityCount = computed(() => {
      return activities.value.filter(activity => !activity.completed).length;
    });
    
    const addActivity = () => {
      if (newActivity.value.trim() === '') return;
      
      const newId = activities.value.length > 0 
        ? Math.max(...activities.value.map(a => a.id)) + 1 
        : 1;
        
      activities.value.push({
        id: newId,
        text: newActivity.value.trim(),
        completed: false
      });
      
      newActivity.value = '';
    };
    
    const deleteActivity = (id) => {
      const index = activities.value.findIndex(activity => activity.id === id);
      if (index !== -1) {
        activities.value.splice(index, 1);
      }
    };

    const toggleComplete = (id) => {
      const activity = activities.value.find(a => a.id === id);
      if (activity) {
        activity.completed = !activity.completed;
      }
    };
    
    return {
      activities,
      newActivity,
      showOnlyIncomplete,
      filteredActivities,
      activeActivityCount,
      addActivity,
      deleteActivity,
      toggleComplete
    };
  }
};
</script>


<style>
:root {
  --primary-color: #4c5af2;
  --secondary-color: #f2f2f2;
  --success-color: #28a745;
  --danger-color: #dc3545;
  --text-color: #333;
  --light-text: #666;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
  background-color: #f5f7fa;
  color: var(--text-color);
  padding: 20px;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 6px 18px rgba(0, 0, 0, 0.1);
  padding: 30px;
}

h1 {
  text-align: center;
  color: var(--primary-color);
  margin-bottom: 20px;
  font-weight: 600;
}

button {
  padding: 12px 20px;
  border: none;
  border-radius: 6px;
  background-color: var(--primary-color);
  color: white;
  cursor: pointer;
  font-size: 16px;
  transition: all 0.3s ease;
}

button:hover {
  background-color: #3a47d5;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.transition-group-enter-active,
.transition-group-leave-active {
  transition: all 0.5s ease;
}

.transition-group-enter-from,
.transition-group-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>