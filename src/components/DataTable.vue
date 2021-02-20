<template>
  <table class="w-full">
    <thead>
      <tr class="bg-gray-100">
        <th
          v-for="column in columns"
          :key="column.name"
          class="border border-gray-300 p-2"
          :class="[column.classNames?.header, visibilityClass(column.visible)]"
        >
          {{ column.label }}
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(record, index) in records" :key="record.id">
        <td
          v-for="column in columns"
          :key="column.name"
          class="border border-gray-300 p-2"
          :class="[column.classNames?.cell, visibilityClass(column.visible)]"
        >
          <slot :name="column.name" v-bind="{ record, records, index, column }"></slot>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "DataTable",
  props: {
    columns: {
      type: Array,
      required: true,
      validator: (records) => records.find(({ name }) => name === undefined) === undefined,
    },
    records: {
      type: Array,
      required: true,
      validator: (records) => records.find(({ id }) => id === undefined) === undefined,
    },
  },
  methods: {
    visibilityClass(visibilityList) {
      if (!Array.isArray(visibilityList)) {
        return null;
      }

      const classMap = {
        sm: {
          [true]: "sm:table-cell",
          [false]: "sm:hidden",
        },
        md: {
          [true]: "md:table-cell",
          [false]: "md:hidden",
        },
        lg: {
          [true]: "lg:table-cell",
          [false]: "lg:hidden",
        },
        xl: {
          [true]: "xl:table-cell",
          [false]: "xl:hidden",
        },
        "2xl": {
          [true]: "2xl:table-cell",
          [false]: "2xl:hidden",
        },
      };

      const classList = ["hidden"];

      for (const breakpoint of visibilityList) {
        const normalizedBreakpoint = breakpoint.replace(/^-/, "");
        const visible = normalizedBreakpoint === breakpoint;

        classList.push(classMap[normalizedBreakpoint][visible]);
      }

      return classList.join(" ");
    },
  },
};
</script>
