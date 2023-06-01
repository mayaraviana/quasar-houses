<template>
  <div>
    <q-table
      :rows="houseRules"
      :columns="columns"
      row-key="id"
      v-model:pagination="pagination"
    >
      <template v-slot:body-cell-actions="props">
        <div class="q-gutter-sm">
          <q-btn
            flat
            dense
            round
            icon="delete"
            size="sm"
            @click="deleteRule(props.row)"
          />
        </div>
      </template>
    </q-table>
  </div>
</template>

<script>
import axios from 'axios';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'TableComponent',
  data() {
    return {
      loggedIn: true,
      houseRules: [],
      columns: [
        {
          name: 'id',
          required: true,
          label: 'ID',
          align: 'left',
          field: 'id',
          sortable: true,
        },
        {
          name: 'name',
          required: true,
          label: 'Name',
          align: 'left',
          field: 'name',
          sortable: true,
        },
        {
          name: 'active',
          required: true,
          label: 'Active',
          align: 'left',
          field: 'active',
          sortable: true,
        },
        {
          name: 'actions',
          label: 'Actions',
          align: 'center',
          field: 'id',
          sortable: false,
        },
      ],
      pagination: {
        rowsPerPage: 10,
      },
    };
  },
  mounted() {
    this.fetchHouseRules();
  },
  methods: {
    fetchHouseRules() {
      const config = {
        headers: {
          Authorization: `Bearer ${process.env.AUTHORIZATION}`,
        },
      };

      axios
        .get(`${process.env.API_URL}/house_rules`, config)
        .then((response) => {
          const responseData = response.data.data;
          this.houseRules = responseData.entities.map((rule) => {
            return {
              ...rule,
              actions: rule.id,
            };
          });
        })
        .catch((error) => {
          console.error(error);
        });
    },
    deleteRule(rule) {
      const config = {
        headers: {
          Authorization: `Bearer ${process.env.AUTHORIZATION}`,
        },
      };

      axios
        .delete(`${process.env.API_URL}/house_rules/${rule.id}`, config)
        .then((response) => {
          const responseData = response.data;
          if (responseData.success) {
            const index = this.houseRules.findIndex((r) => r.id === rule.id);
            if (index !== -1) {
              this.houseRules.splice(index, 1);
              this.$emit('ruleDeleted', rule.id);
            }
          } else {
            console.error(responseData.message);
          }
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
});
</script>
