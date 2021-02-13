<template>
  <div class="rounded-md shadow-md border border-gray-300">
    <table class="w-full">
      <thead>
        <tr>
          <template v-for="column in columns">
            <th
              v-if="column.sort"
              :key="column.name"
              :class="[
                column.headingClass,
                sortedColumn === column.sort ? 'font-medium' : 'font-normal',
                visibilityClass(column.visibility),
              ]"
              class="uppercase"
            >
              <button
                type="button"
                @click="
                  $emit('setSort', sort === column.sort ? descending(column.sort) : column.sort)
                "
              >
                {{ column.label }}
                <span v-if="sort === column.sort" class="text-xs">asc</span>
                <span v-if="sort === descending(column.sort)" class="text-xs">desc</span>
              </button>
            </th>
            <th
              v-else
              :key="column.name"
              :class="[column.headingClass, visibilityClass(column.visibility)]"
              class="uppercase font-normal"
            >
              {{ column.label }}
            </th>
          </template>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(record, index) in records" :key="record.id" class="border-t border-gray-300">
          <td v-for="column in columns" :key="column.name">
            <slot :name="column.name" v-bind="{ record, records, index }" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "ResponsiveTable",
  props: {
    sort: {
      type: String,
      default: undefined,
    },
    columns: {
      type: Array,
      required: true,
    },
    records: {
      type: Array,
      required: true,
    },
  },

  computed: {
    sortedColumn() {
      return this.normaliseColumn(this.sort);
    },
  },

  methods: {
    descending(sort) {
      return `-${sort}`;
    },

    visibilityClass(spec) {
      if (!Array.isArray(spec) || spec.length === 0) {
        return null;
      }

      return spec.reduce((className, breakpoint) => {
        const normalisedBreakpoint = this.normaliseColumn(breakpoint);
        const displayClass = normalisedBreakpoint === breakpoint ? "table-cell" : "hidden";

        return `${className} ${normalisedBreakpoint}:${displayClass}`;
      }, "hidden");
    },

    normaliseColumn(column) {
      return column?.replace(/^-/, "");
    },
  },
};
</script>
