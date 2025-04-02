<template>
  <div class="flex flex-col flex-grow justify-center items-center bg-no-repeat bg-cover bg-center" 
       style="background-image: url('/images/Mortal.png'); background-size: cover; height: 100vh;">
    
   
    <div class="overflow-y-auto max-h-screen w-full p-6">
      
      
      <NuxtLink to="Lab4" class="text-3xl bg-red-950 text-white min-w-16 h-16 rounded-xl hover:bg-red-300 hover:text-black border-2 border-black mb-4">
        Lab Before
      </NuxtLink>
      
    
      <label for="select" class="text-3xl bg-red-950 text-white min-w-16 h-16 rounded-xl hover:bg-red-300 hover:text-black border-2 border-black mb-4">Choose the character</label>
      <select id="select" v-model="selectus" class="border p-2 rounded mb-4 w-full">
        <option value="Raiden">Raiden</option>
        <option value="Scorp">Scorpion</option>
        <option value="Sub-Zero">Sub-Zero</option>
        <option value="Motaro">Motaro</option>
      </select>
      
      
      <div class="flex" v-if="selectus === 'Raiden'"><Raiden /></div>
      <div class="flex" v-else-if="selectus === 'Scorp'"><Scorp /></div>
      <div class="flex" v-else-if="selectus === 'Sub-Zero'"><SubZero /></div>
      <div class="flex" v-else-if="selectus === 'Motaro'"><Motaro /></div>
      
      <label for="select" class="text-3xl bg-red-950 text-white min-w-16 h-16 rounded-xl hover:bg-red-300 hover:text-black border-2 border-black mb-4">Find the character</label>
      <input name="filter" v-model="search" placeholder="Search characters" class="border p-2 rounded mb-4 w-full">
      <div v-for="(image, index) in finder" :key="index" class="flex justify-center mb-4">
        <img :src="image.image" class="w-32 h-32 object-cover rounded">
      </div>
      
      <label for="select" class="text-3xl bg-red-950 text-white min-w-16 h-16 rounded-xl hover:bg-red-300 hover:text-black border-2 border-black mb-4">Mortal Kombat Calculator</label>
      <form class="flex flex-col gap-4 mb-4 w-full">
        <div class="flex flex-col">
          <label for="frst" class="font-semibold text-white">Enter the first number</label>
          <input name="frst" type="number" v-model.number="frst" class="border p-2 rounded w-full">
        </div>
        <div class="flex flex-col">
          <label for="scnd" class="font-semibold text-white">Enter the second number</label>
          <input name="scnd" type="number" v-model.number="scnd" class="border p-2 rounded w-full">
        </div>
      </form>

     
      <div class="flex gap-4 mb-4 w-full justify-center">
        <button @click="set_sign('*')" class="text-3xl bg-red-950 text-white min-w-16 h-16 rounded-xl hover:bg-red-300 hover:text-black border-2 border-black">*</button>
        <button @click="set_sign('/')" class="text-3xl bg-red-950 text-white min-w-16 h-16 rounded-xl hover:bg-red-300 hover:text-black border-2 border-black">/</button>
        <button @click="set_sign('+')" class="text-3xl bg-red-950 text-white min-w-16 h-16 rounded-xl hover:bg-red-300 hover:text-black border-2 border-black">+</button>
        <button @click="set_sign('-')" class="text-3xl bg-red-950 text-white min-w-16 h-16 rounded-xl hover:bg-red-300 hover:text-black border-2 border-black">-</button>
      </div>
      
     
      <p class="text-xl text-white mt-4">Result is: {{ calc }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, reactive } from "vue";


const selectus = ref<string>('Raiden');
const search = ref<string>('');
const signn = ref<string>('+');
const frst = ref<number>(0);
const scnd = ref<number>(0);


interface Stking {
  name: string;
  image: string;
}

const filtering = reactive<Stking[]>([
  { name: 'Motaro', image: "/images/Motaro.jpg" },
  { name: 'Raiden', image: "/images/Raiden.jpg" },
  { name: 'SubZero', image: "/images/SubZero.jpg" },
  { name: 'Scorpion', image: "/images/Scorpion.jpg" },
]);


const finder = computed(() => {
  return filtering.filter(img => img.name.toLowerCase().includes(search.value.toLowerCase()));
});


const set_sign = (op: string): void => {
  signn.value = op;
};


const calc = computed((): number => {
  switch (signn.value) {
    case "*":
      return frst.value * scnd.value;
    case "/":
      return scnd.value !== 0 ? parseFloat((frst.value / scnd.value).toFixed(1)) : 0;
    case "+":
      return frst.value + scnd.value;
    case "-":
      return frst.value - scnd.value;
    default:
      return 0;
  }
});
</script>
