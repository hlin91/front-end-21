<template>
  <div>
    <v-row justify="center">
      <h2 class="font-weight-light pr-2">Vehicle Mission Stage:</h2>
      <h2 class="font-weight-regular pb-2">ERU Drop</h2>
    </v-row>
    <div
      style="
        display: grid;
        grid-template-columns: auto auto auto auto auto;
        grid-gap: 5px;
        padding-bottom: 15px;
      "
    >
      <div v-for="(mea_data, index) in mea_data" :key="index">
        <div style="display: flex; padding-right: 3px">
          <h4 class="font-weight-regular pr-1">{{ mea_data.title }}:</h4>
          <h4 class="font-weight-bold" style="float: right">
            {{ mea_data.value }}
          </h4>
        </div>
      </div>
    </div>

    <v-row justify="left">
      <h3 class="font-weight-bold">Messages:</h3>
    </v-row>
    <v-row fluid justify="center">
      <v-col :cols="12">
        <div
          class="scrollable"
          style="border: 1px solid #bfbfbf; font-size: small; border-radius: 5px; height: 65px; overflow-y: hidden;
          "
        >
          <div v-for="(mea_messages, index) in mea_messages" :key="index">
            <p class="my-0 py-0 px-1">{{ mea_messages.message }}</p>
          </div>
        </div>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  //either props or in data MOST LIKELY DATA
  data() {
    return {
      mea_data: [],
      mea_messages: [],
      //mission_status
      //battery
    };
  },
  mounted() {
    fetch("http://localhost:3000/mea_data")
      .then((res) => res.json())
      .then((data) => (this.mea_data = data))
      .catch((err) => console.log(err.message));
    fetch("http://localhost:3000/mea_messages")
      .then((res) => res.json())
      .then((data) => (this.mea_messages = data))
      .catch((err) => console.log(err.message));
  },
};
</script>
<style>
.scrollable:hover,
.scrollable:active,
.scrollable:focus {
  overflow-y: auto !important;
}
</style>