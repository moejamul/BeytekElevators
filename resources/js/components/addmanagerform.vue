<template>
  <form method="POST" @submit.prevent="submit" style="padding: 3em">
    <!-- @submit.prevent="submit" is calling the submit method defined in the script below -->
    <div class="form-row">
      <div class="form-group col-md-6">
        <label for="inputEmail4">Manager Name</label>
        <input
          class="form-control"
          v-model="fields.name"
          placeholder="Manager Name"
        />
        <!-- v-model is used to get the input values, and only works in input elements, fields
      is defined in the script below.
      "name" is one of the required attributes for us to do a post request through the API, it will be passed through
      fields, as written in the script below -->
      </div>
      <div class="form-group col-md-6">
        <label for="inputPassword4">Address</label>
        <input
          class="form-control"
          v-model="fields.address"
          placeholder="Address"
        />
      </div>
    </div>

    <div class="form-row">
      <div class="form-group col-md-6">
        <label for="inputEmail4">Phone Number</label>
        <input
          class="form-control"
          v-model="fields.phone_number"
          placeholder="Phone Number"
        />
      </div>
      <div class="form-group col-md-6">
        <label for="inputPassword4"
          >Profile Picture (should have been an upload)</label
        >
        <input
          class="form-control"
          v-model="fields.profile_picture"
          placeholder="Profile Picture"
        />
      </div>
    </div>
    <button type="submit" class="btn btn-primary">Add</button>
  </form>
</template>


<script>
export default {
  data() {
    return {
      fields: {},
    };
  },
  methods: {
    submit() {
      axios
        .post(
          "http://localhost/beytekelevators/public/api/addmanager",
          this.fields
        )
        .then((response) => {
          this.fields = {};
          this.success = true;
          this.errors = {};
        })
        .catch((error) => {
          if (error.response.status == 422) {
            this.errors = error.response.data.errors;
          }
          console.log("Error");
        });
    },
  },
};
</script>