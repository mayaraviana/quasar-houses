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

    <TableComponent @ruleDeleted="updateRuleList" />
  </div>
</template>

<script>
import TableComponent from './../components/TableComponent.vue';

export default {
  components: {
    TableComponent,
  },
  data() {
    return {
      loggedIn: true,
      rules: [],
    };
  },
  methods: {
    updateRuleList(ruleId) {
      this.rules = this.rules.filter((rule) => rule.id !== ruleId);
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
