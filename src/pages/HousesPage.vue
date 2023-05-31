<template>
  <div class="house-rules">
    <div class="q-pa-md q-mb-md">
      <div class="row">
        <div class="col-md-8">
          <h1>House rules - The cove on milsons</h1>
          <p>
            Thank you for choosing our platform to list your property. To ensure
            a pleasant and comfortable experience for your guests, it is
            important to establish clear house rules. Please take a moment to
            define the house rules for your property below:
          </p>
          <q-btn
            unelevated
            color="primary"
            text-color="white"
            icon="add"
            label="New rule"
            class="login-button"
          />
        </div>
      </div>
    </div>

    <q-table
      :rows="houseRules"
      :columns="columns"
      row-key="id"
      :pagination="true"
      :rows-per-page-options="[10]"
      @request="fetchHouseRules"
    ></q-table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
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
        // Add other columns as needed
      ],
      pagination: {
        total: 0,
        count: 0,
        per_page: 10,
        current_page: 1,
        total_pages: 1,
      },
    };
  },
  mounted() {
    this.fetchHouseRules();
  },
  methods: {
    fetchHouseRules(request) {
      const page = request ? request.pagination.page : 1;
      const limit = request ? request.pagination.rowsPerPage : 10;

      const config = {
        headers: {
          Authorization: `Bearer ${process.env.AUTHORIZATION}`,
        },
        params: {
          page: page - 1,
          limit: limit,
        },
      };

      axios
        .get(`${process.env.API_URL}/house_rules`, config)
        .then((response) => {
          const responseData = response.data.data;
          this.houseRules = responseData.entities;
          this.pagination = responseData.pagination;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style scoped>
.house-rules {
  max-width: 1200px;
  margin: 0 auto;
}
h1 {
  font-weight: 600;
  font-size: 1.875rem;
  line-height: 150%;
  color: #101828;
}
p {
  font-size: 1rem;
  line-height: 150%;
  color: #667085;
}
</style>
