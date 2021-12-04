<template>
  <div>
    <form @submit.prevent="searchForStuff">
      <input type="text" v-model="searchText" />
      <button>Search For TV Shows</button>
    </form>
    <div class="stuff">
      <div v-for="show in myData" :key="show.id">
        <img :src="show.show?.image?.medium" alt="image"/>
      </div>
    </div>
  </div>
</template> 
<script lang="ts">
export default {
  layout: "custom",
};
</script>
<script setup lang="ts">
// useFetch 사용법
// const { data }: { data: any } = await useFetch("/api/tv?search=girls", {});
// useAsyncData 사용법
// const { data } = await useAsyncData("searchData", () => {
//   return $fetch("/api/tv?search=mash");
// });
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