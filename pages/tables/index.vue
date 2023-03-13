<template>
  <div>
    <div class="text-3xl text-center" v-if="pending">Loading...</div>
    <div v-else>
      <table class="border-collapse w-full">
        <thead class="bg-gray-50 border-b-2 border-gray-200">
          <tr>
            <th
              class="cursor-pointer p-3 font-bold uppercase bg-gray-200 text-gray-600 border-gray-300 hidden lg:table-cell"
              @click="sortData('name')"
            >
              Name
              <Icon
                v-if="currentSorting === 'name'"
                :name="asc ? 'mdi:arrow-up' : 'mdi:arrow-down'"
              />
            </th>
            <th
              class="cursor-pointer p-3 font-bold uppercase bg-gray-200 text-gray-600 border-gray-300 hidden lg:table-cell"
              @click="sortData('birth_year')"
            >
              Birth Year
              <Icon
                v-if="currentSorting === 'birth_year'"
                :name="asc ? 'mdi:arrow-up' : 'mdi:arrow-down'"
              />
            </th>
            <th
              class="cursor-pointer p-3 font-bold uppercase bg-gray-200 text-gray-600 border-gray-300 hidden lg:table-cell"
              @click="sortData('gender')"
            >
              Gender
              <Icon
                v-if="currentSorting === 'gender'"
                :name="asc ? 'mdi:arrow-up' : 'mdi:arrow-down'"
              />
            </th>
            <th
              class="cursor-pointer p-3 font-bold uppercase bg-gray-200 text-gray-600 border-gray-300 hidden lg:table-cell"
              @click="sortData('eye_color')"
            >
              Eye Color
              <Icon
                v-if="currentSorting === 'eye_color'"
                :name="asc ? 'mdi:arrow-up' : 'mdi:arrow-down'"
              />
            </th>
            <th
              class="cursor-pointer p-3 font-bold uppercase bg-gray-200 text-gray-600 border-gray-300 hidden lg:table-cell"
            >
              Actions
            </th>
          </tr>
        </thead>
        <tbody class="divide-y divide-gray-100">
          <template v-for="(person, index) in people.results" :key="person.url">
            <tr
              class="bg-white lg:hover:bg-gray-100 flex lg:table-row flex-row lg:flex-row flex-wrap lg:flex-no-wrap mb-5 lg:mb-0"
            >
              <td
                class="w-full lg:w-auto p-3 text-gray-800 text-center border-b block lg:table-cell relative lg:static"
              >
                <nuxtLink
                  :to="`/tables/${page * 10 - 10 + index + 1}`"
                  class="cursor-pointer underline"
                >
                  {{ person.name }}
                </nuxtLink>
              </td>
              <td
                class="w-full lg:w-auto p-3 text-gray-800 text-center border-b block lg:table-cell relative lg:static"
              >
                {{ person.birth_year }}
              </td>
              <td
                class="w-full lg:w-auto p-3 text-gray-800 text-center border-b block lg:table-cell relative lg:static"
              >
                {{ person.gender }}
              </td>
              <td
                class="w-full lg:w-auto p-3 text-gray-800 text-center border-b block lg:table-cell relative lg:static"
              >
                {{ person.eye_color }}
              </td>
              <td
                class="w-full lg:w-auto p-3 text-gray-800 text-center border-b block lg:table-cell relative lg:static"
                @click="toggle(person.url)"
              >
                <Icon
                  class="cursor-pointer"
                  :name="
                    opened.includes(person.url)
                      ? 'mdi:chevron-up'
                      : 'mdi:chevron-down'
                  "
                />
              </td>
            </tr>
            <tr
              class="bg-gray-300 lg:hover:bg-gray-100 flex lg:table-row flex-row lg:flex-row flex-wrap lg:flex-no-wrap mb-5 lg:mb-0"
              v-if="opened.includes(person.url)"
            >
              <td
                class="w-full lg:w-auto p-3 text-gray-800 text-center border-b block lg:table-cell relative lg:static"
              >
                <span class="font-bold"> Height: </span>
                {{ person.height }}
              </td>
              <td
                class="w-full lg:w-auto p-3 text-gray-800 text-center border-b block lg:table-cell relative lg:static"
              >
                <span class="font-bold"> Skin Color: </span>
                {{ person.skin_color }}
              </td>
              <td
                colspan="3"
                class="w-full lg:w-auto p-3 text-gray-800 text-center border-b block lg:table-cell relative lg:static"
              >
                <span class="font-bold"> Mass: </span>
                {{ person.mass }}
              </td>
            </tr>
          </template>
        </tbody>
      </table>
      <Pagination @change="refetch" :totalPages="9" :currentPage="page" />
    </div>
  </div>
</template>

<script setup lang="ts">
// Interface of SWAPI response
interface People {
  results: {
    birth_year: string;
    created: string;
    edited: string;
    eye_color: string;
    films: string[];
    gender: string;
    hair_color: string;
    height: string;
    homeworld: string;
    mass: string;
    name: string;
    skin_color: string;
    species: string[];
    starships: string[];
    url: string;
    vehicles: string[];
  }[];
  count: Number;
  next: string;
  previous: string;
}

// Page number stored for smart back
const page = useState<Number>("page", () => 1);

// Array to store expanded rows
let opened: string[] = [];

// Sorting variables
let currentSorting: string = "";
let asc: boolean = true;
let sort: string = "id";

const {
  data: people,
  refresh,
  pending,
} = await useFetch<People>(
  () => `https://swapi.dev/api/people/?page=${page.value}`,
  {
    key: `page-${page.value}`,
  }
);

function refetch(pageNumber: number) {
  page.value = pageNumber;
  refresh();
}

function sortData(attribute: string) {
  currentSorting = attribute;
  if (asc)
    people.value!.results = people.value!.results.sort(
      (a: { [x: string]: number }, b: { [x: string]: number }) => {
        if (a[attribute] > b[attribute]) return 1;
        if (a[attribute] < b[attribute]) return -1;
        return 0;
      }
    );
  else
    people.value!.results = people.value!.results.sort(
      (a: { [x: string]: number }, b: { [x: string]: number }) => {
        if (a[attribute] < b[attribute]) return 1;
        if (a[attribute] > b[attribute]) return -1;
        return 0;
      }
    );
  asc = !asc;
}

function toggle(id: string) {
  const index = opened.indexOf(id);
  if (index > -1) {
    opened.splice(index, 1);
  } else {
    opened.push(id);
  }
  refresh();
}
</script>
