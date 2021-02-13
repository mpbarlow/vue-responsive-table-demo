<template>
  <div class="container mx-auto px-4 my-12">
    <ResponsiveTable class="w-full" v-bind="{ records, columns, sort }" @setSort="sort = $event">
      <template #a="{ record }">
        <div class="flex flex-col">
          <span class="text-xs md:hidden text-blue-500">{{ record.b }}</span>
          <span class="text-red-500">{{ record.a }}</span>
          <span class="text-xs sm:hidden">
            <span class="text-green-500">{{ record.c }}</span>
            <span class="text-pink-500">{{ record.d }}</span>
          </span>
        </div>
      </template>

      <template #b="{ record }">{{ record.b }}</template>

      <template #c="{ record }">
        <div class="flex flex-col">
          <span class="text-xs md:hidden text-pink-500">{{ record.d }}</span>
          <span class="text-green-500">{{ record.c }}</span>
        </div>
      </template>

      <template #d="{ record }">{{ record.d }}</template>
    </ResponsiveTable>
  </div>
</template>

<script>
import ResponsiveTable from "./components/ResponsiveTable.vue";

export default {
  name: "App",
  components: {
    ResponsiveTable,
  },

  data() {
    return {
      sort: "a",
      records: [
        { id: 1, a: "1a", b: "1b", c: "1c", d: "1d" },
        { id: 2, a: "2a", b: "2b", c: "2c", d: "2d" },
        { id: 3, a: "3a", b: "3b", c: "3c", d: "3d" },
        { id: 4, a: "4a", b: "4b", c: "4c", d: "4d" },
      ],
      columns: [
        {
          name: "a",
          label: "One",
          headingClass: "text-red-500",
          sort: "a",
          visibility: ["md", "-lg", "xl"],
        },
        {
          name: "b",
          label: "Two",
          headingClass: "text-blue-500",
          sort: "b",
        },
        {
          name: "c",
          label: "Three",
          headingClass: "text-green-500",
        },
        {
          name: "d",
          label: "Four",
          headingClass: "text-pink-500",
        },
      ],
    };
  },
};
</script>
