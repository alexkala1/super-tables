<template>
  <div>
    <table class="w-full table-auto">
      <thead class="bg-gray-50 border-b-2 border-gray-200">
        <tr>
          <th
            class="p-3 text-gray-900 text-sm font-semibold tracking-wide text-left"
            @click="
              people.results.sort((a, b) => a.url < b.url);
              refresh();
            "
          >
            ID
          </th>
          <th
            class="p-3 text-gray-900 text-sm font-semibold tracking-wide text-left"
            @click="sortData(name, people.results)"
          >
            Name
          </th>
          <th
            class="p-3 text-gray-900 text-sm font-semibold tracking-wide text-left"
            @click="
              people.results.sort((a, b) => a.birth_year < b.birth_year);
              refresh();
            "
          >
            Birth Year
          </th>
          <th
            class="p-3 text-gray-900 text-sm font-semibold tracking-wide text-left"
            @click="
              people.results.sort((a, b) => a.gender < b.gender);
              refresh();
            "
          >
            Gender
          </th>
          <th
            class="p-3 text-gray-900 text-sm font-semibold tracking-wide text-left"
            @click="
              people.results.sort((a, b) => a.eye_color < b.eye_color);
              refresh();
            "
          >
            Eye Color
          </th>
          <th
            class="p-3 text-gray-900 text-sm font-semibold tracking-wide text-left"
          >
            Actions
          </th>
        </tr>
      </thead>
      <tbody class="divide-y divide-gray-100">
        <template
          v-for="(person, index) in people.results"
          :key="page * 10 - 10 + index + 1"
        >
          <tr class="bg-white">
            <td class="p-3 text-sm text-gray-700 whitespace-nowrap">
              <nuxtLink :to="`/table/${page * 10 - 10 + index + 1}`">{{
                page * 10 - 10 + index + 1
              }}</nuxtLink>
            </td>
            <td class="p-3 text-sm text-gray-700 whitespace-nowrap">
              {{ person.name }}
            </td>
            <td class="p-3 text-sm text-gray-700 whitespace-nowrap">
              {{ person.birth_year }}
            </td>
            <td class="p-3 text-sm text-gray-700 whitespace-nowrap">
              {{ person.gender }}
            </td>
            <td class="p-3 text-sm text-gray-700 whitespace-nowrap">
              {{ person.eye_color }}
            </td>
            <td
              class="p-3 text-sm text-gray-700 whitespace-nowrap"
              @click="toggle(page * 10 - 10 + index + 1)"
            >
              <Icon
                :name="
                  opened.includes(page * 10 - 10 + index + 1)
                    ? 'mdi:chevron-up'
                    : 'mdi:chevron-down'
                "
              />
            </td>
          </tr>
          <tr
            class="bg-gray-500"
            v-if="opened.includes(page * 10 - 10 + index + 1)"
          >
            <td colspan="6">
              <div class="flex px-10 py-5">
                <div class="flex-none w-64">
                  <span class="font-bold"> Height: </span>
                  {{ person.height }}
                </div>
                <div class="flex-initial w-64">
                  <span class="font-bold"> Mass: </span>
                  {{ person.mass }}
                </div>
                <div class="flex-initial w-64">
                  <span class="font-bold"> Skin Color: </span>
                  {{ person.skin_color }}
                </div>
              </div>
            </td>
          </tr>
        </template>
      </tbody>
    </table>
    <Pagination @change="refetch" :totalPages="9" :currentPage="page" />
  </div>
</template>

<script setup>
const page = useState("page", () => 1);
let opened = [];
let previousSort = "";
let sort = "id";
const { data: people, refresh } = await useFetch(
  () => `https://swapi.dev/api/people/?page=${page.value}`,
  {
    key: `page-${page.value}`,
  }
);

function refetch(pageNumber) {
  page.value = pageNumber;
  refresh();
}

function sortList(sortMethod) {
  // console.log(sort, previousSort, sortMethod);
  // if (sortMethod === previousSort) {
  //   people.results = people.results.sort((a, b) => {
  //     descending = !descending;
  //     if (descending) return a[sortMethod] - b[sortMethod];
  //     else return b[sortMethod] - a[sortMethod];
  //   });
  // }
  // previousSort = sort;
  // sort = sortMethod;
  console.log(people._rawValue);
  people.results = people._rawValue.results.sort((a, b) => a.name < b.name);

  refresh();
}

function sortData(name, people) {
  let peoples = people.sort((a, b) => a.name < b.name);
  console.log(peoples[0].name);
  console.log(peoples);

  return peoples;
}

function toggle(id) {
  const index = opened.indexOf(id);
  console.log(id, opened, index);
  if (index > -1) {
    opened.splice(index, 1);
  } else {
    opened.push(id);
  }
  refresh();
}
</script>

<style lang="scss" scoped></style>
