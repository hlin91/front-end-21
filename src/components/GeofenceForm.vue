<template>
<div>
    <h1 class="font-weight-light" pa-0 ma-0>Geofence</h1>
    <validation-observer
    ref="observer"
    v-slot="{ invalid }"
  >
    <form @submit.prevent="submit" class="scrollable" style="height: 250px; overflow-y: hidden; overflow-x: hidden;">
        <KeepInSwitch />
      <v-container>
          <v-form v-for="(input,k) in inputs" :key="k">
          <v-row>
              <v-col cols="5">
                <validation-provider
                    v-slot="{ errors }"
                    name="Latitude"
                    :rules="{
                    required: true,
                    }"
                    class="pa-0 ma-0"
                >
                    <v-text-field
                    v-model="input.longitude"
                    :error-messages="errors"
                    label="Latitude"
                    required
                    ></v-text-field>
                </validation-provider>
              </v-col>
              <v-col cols="5">
                <validation-provider
                    v-slot="{ errors }"
                    name="Longitude"
                    :rules="{
                    required: true,
                    }"
                >
                    <v-text-field
                    v-model="input.latitude"
                    :error-messages="errors"
                    label="Longitude"
                    required
                    ></v-text-field>
                </validation-provider>
              </v-col>
              <v-col :cols="1">
                  <v-icon class="mt-2" color="green" @click="add(k)" v-show="k == inputs.length-1">mdi-plus-circle</v-icon>
              </v-col>
              <v-col :cols="1">
                  <v-icon class="mt-2" color="red" @click="remove(k)" v-show="k || ( !k && inputs.length > 1)">mdi-minus-circle</v-icon>
              </v-col>
          </v-row>
          </v-form>
          <v-row>
            <v-btn
                class="mr-4"
                color="green"
                type="submit"
                :disabled="invalid"
            >
                Submit
            </v-btn>
            <v-btn>
                Delete 
            </v-btn>
          </v-row>
      </v-container>
    </form>
  </validation-observer>
</div>
</template>

<script>
  import { required, minValue } from 'vee-validate/dist/rules'
  import { extend, ValidationObserver, ValidationProvider, setInteractionMode } from 'vee-validate'
  import KeepInSwitch from '@/components/KeepInSwitch.vue'

  setInteractionMode('eager')

  extend('required', {
    ...required,
    message: '{_field_} cannot be empty',
  })

  export default {
    components: {
      ValidationProvider,
      ValidationObserver,
      KeepInSwitch
    },
    data: () => ({
        inputs: [{
            longitude: '',
            latitude: ''
      }]
    }),

    methods: {
      submit () {
        this.$refs.observer.validate()
      },
      add () {
        this.inputs.push({
        longitude: '',
        latitude: ''
      })
      },
      remove () {
        this.inputs.pop()
      }
    },
  }
</script>
<style>
.scrollable:hover, .scrollable:active, .scrollable:focus {
  overflow-y: auto !important;
}
</style>