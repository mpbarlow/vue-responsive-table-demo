<template>
  <div class="container mx-auto px-4 my-12">
    <DataTable class="w-full" v-bind="{ columns, records }">
      <template #avatar="{ record }">
        <img
          :src="record.avatar"
          alt="A random puppy from Unsplash"
          class="inline-block rounded-full shadow border-2 border-white"
        />
      </template>
      <template #name="{ record }">
        <div class="flex items-center">
          <img
            :src="record.avatar"
            alt="A random puppy from Unsplash"
            class="inline-block md:hidden rounded-full shadow border-2 border-white mr-2"
          />
          <div>
            {{ record.name }}
            <span class="block md:hidden text-gray-600 text-sm">
              {{ record.email }}
              <span class="sm:hidden">&bull; Last login {{ record.last_login }}</span>
            </span>
          </div>
        </div>
      </template>
      <template #email="{ record }">{{ record.email }}</template>
      <template #last_login="{ record }">{{ record.last_login }}</template>
    </DataTable>
  </div>
</template>

<script>
import DataTable from "./components/DataTable.vue";

export default {
  name: "App",
  components: { DataTable },

  data() {
    return {
      records: [
        {
          id: 1,
          avatar:
            "https://images.unsplash.com/photo-1612159841306-e95c7f6dae44?crop=entropy&fit=crop&fm=jpg&h=50&q=80&w=50",
          name: "Rachel Jones",
          email: "rjones@example.com",
          last_login: "2 minutes ago",
        },
        {
          id: 2,
          avatar:
            "https://images.unsplash.com/photo-1611688298941-f2a508ee1c9b?crop=entropy&fit=crop&fm=jpg&h=50&q=80&w=50",
          name: "Faye Knight",
          email: "faye.knight@example.org",
          last_login: "4 days ago",
        },
        {
          id: 3,
          avatar:
            "https://images.unsplash.com/photo-1612195665612-30c359370759?crop=entropy&fit=crop&fm=jpg&h=50&q=80&w=50",
          name: "Joanne Murphy",
          email: "jmurph11@example.net",
          last_login: "yesterday",
        },
      ],
      columns: [
        {
          name: "avatar",
          label: "",
          classNames: {
            cell: "text-center",
          },
          visible: ["md"],
        },
        {
          name: "name",
          label: "Name",
          classNames: {
            header: "text-left",
          },
          sort: "name",
        },
        {
          name: "email",
          label: "Email",
          classNames: {
            header: "text-left",
          },
          visible: ["md"],
        },
        {
          name: "last_login",
          label: "Last Login",
          classNames: {
            cell: "text-center",
          },
          sort: "last_login_date",
          visible: ["sm"],
        },
      ],
    };
  },
};
</script>
