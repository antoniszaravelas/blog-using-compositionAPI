<template>
  <h1>posts</h1>
  <h1 v-if="error">{{ error }}</h1>

  <div v-if="data">
    <div v-for="dat in newArray" :key="dat.id">
      <h1>{{ dat.title }}</h1>
      <button @click="($event) => handleClick(dat.id, $event)">
        Deletionarion
      </button>
    </div>
  </div>
</template>

<script>
import { computed, ref } from 'vue';
export default {
  components: {},
  setup() {
    const data = ref(null);
    const error = ref(null);
    const deleteId = ref(null);

    const loadData = async () => {
      try {
        const temporary = await fetch('http://localhost:3000/jobs');
        if (!temporary.ok)
          throw new Error('there was a problem fetching the data');
        data.value = await temporary.json();
      } catch (err) {
        error.value = err.message;
      }
    };

    loadData();

    const handleClick = (id) => (deleteId.value = id);

    const newArray = computed(() => {
      return data.value.filter((x) => x.id !== deleteId.value);
    });

    return { data, error, loadData, handleClick, newArray };
  },
};
</script>

<style></style>
