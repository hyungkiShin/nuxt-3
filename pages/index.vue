<template>
  <div>
    <form @submit.prevent="searchForStuff">
      <input type="text" v-model="searchText" />
      <button>Search For TV Shows</button>
    </form>
    <div class="stuff">
      <div v-for="item in myData" :key="item.id">
        <img v-if="isImage(item)" :src="item.show?.image?.medium" alt="image"/>
      </div>
    </div>
  </div>
</template> 
<script lang="ts">
export default {
  layout: "custom",
  methods: {
    isImage(item) {
      return item.show?.image?.medium
    }
  }
};
</script>
<script setup lang="ts">
import { ref } from "vue";
const searchText = ref("");
const myData = ref([]) as any;
async function searchForStuff() {
  const data = await fetch(`/api/tv?search=${searchText.value}`);
  const json = await data.json();
  console.log("json", json);
  myData.value = json;
}
</script> 
<style>
.stuff {
  margin-top: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  /* flex-direction: column; */
  gap: 10px;
}
.form {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 100px;
}
</style>