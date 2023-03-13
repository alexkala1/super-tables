<template>
  <div class="grid grid-cols-1 lg:grid-cols-3 gap-4 w-full">
    <div class="rounded shadow-lg bg-gray-200 text-black p-5">
      <h1 class="font-bold text-xl mb-2">Basic characteristics</h1>
      <ul>
        <li class="py-2 text-gray-700">
          <span class="font-bold">Name:</span> {{ person.name }}
        </li>
        <li class="py-2 text-gray-700">
          <span class="font-bold">Height:</span> {{ person.height }}
        </li>
        <li class="py-2 text-gray-700">
          <span class="font-bold">Hair color:</span> {{ person.hair_color }}
        </li>
        <li class="py-2 text-gray-700">
          <span class="font-bold">Mass:</span> {{ person.mass }}
        </li>
        <li class="py-2 text-gray-700">
          <span class="font-bold">Skin color:</span> {{ person.skin_color }}
        </li>
        <li class="py-2 text-gray-700">
          <span class="font-bold">Eye color:</span> {{ person.eye_color }}
        </li>
        <li class="py-2 text-gray-700">
          <span class="font-bold">Gender:</span> {{ person.gender }}
        </li>
      </ul>
    </div>
    <div class="rounded shadow-lg bg-gray-200 text-black p-5">
      <div class="mb-2" v-if="person.homeworld">
        <h1 class="font-bold text-xl mb-2">Home World</h1>
        <a :href="person.homeworld" class="text-blue-500 underline">
          {{ person.homeworld }}
        </a>
      </div>
      <div class="mb-2" v-if="person.species.length > 0">
        <h1 class="font-bold text-xl mb-2">Species</h1>
        <div v-for="(specimen, index) in person.species" :key="index">
          <a :href="person.homeworld" class="text-blue-500 underline">
            {{ specimen }}
          </a>
        </div>
      </div>
      <div class="mb-2" v-if="person.vehicles.length > 0">
        <h1 class="font-bold text-xl mb-2">Vehicles</h1>
        <div v-for="(vechicle, index) in person.vehicles" :key="index">
          <a :href="person.homeworld" class="text-blue-500 underline">
            {{ vechicle }}
          </a>
        </div>
      </div>
      <div class="mb-2" v-if="person.starships.length > 0">
        <h1 class="font-bold text-xl mb-2">Starships</h1>
        <div v-for="(starship, index) in person.starships" :key="index">
          <a :href="person.homeworld" class="text-blue-500 underline">
            {{ starship }}
          </a>
        </div>
      </div>
    </div>
    <div class="rounded shadow-lg bg-gray-200 text-black p-5">
      <h1 class="font-bold text-xl mb-2">Movies</h1>
      <div v-for="(film, index) in person.films" :key="index">
        <a :href="person.homeworld" class="text-blue-500 underline">
          {{ film }}
        </a>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const { id } = useRoute().params;

const { data: person } = await useFetch(`https://swapi.dev/api/people/${id}`);
</script>
