<!--BİSMİLLAH-->
<template>
  <input @keydown.enter="post" type="text" v-model="title">

  <div class="container">
    <div class="text-right mr-5 mt-3 text-3xl">{{ clock }}</div>
    <div class="mt-10">
      <select class="appearance-none text-3xl outline-0 border-b rounded-2xl border-rose-400 text-center flex m-auto active:border-gray-500 mb-5">
        <option class="" v-for="item in cities" :key="item.id">{{ item.name }}</option>
      </select>
      <div class="grid grid-cols-3 gap-5 ml-3 mr-3">
        <div v-for="i in 6" :key="i" class="active:bg-red-600 flex rounded-xl h-40 bg-gray-300">
          <div class="flex ml-5 mr-5 gap-[120%]">
            <h3 class="flex text-4xl items-center">sabah</h3>
            <p class="flex items-center text-3xl">3:27</p>
          </div>
        </div>
      </div>
      <div class="flex w-full bg-sky-300 mt-5 justify-center items-center gap-[30%]">
        <h2 class="text-5xl">sabah</h2>
        <img src="@/assets/hayrat.png" alt="logo">
        <h2 class="text-5xl">0:30</h2>
      </div>
    </div>
  </div>

</template>


<script setup>
import moment from "moment"
import {onMounted, ref, inject} from "vue";

const title = ref()
const name = ref([])
const appAxios = inject("appAxios")
const clock = ref()
const cities = ref([])
const updateClock = () => {
  const currentTime = moment().format('HH:mm');
  clock.value = currentTime

};

onMounted(() => {
  updateClock();
});

setInterval(() => {
  updateClock();
}, 1500);

appAxios.get("/city").then(response_city => {
  console.log(response_city)
  cities.value = response_city.data || []
})


</script>