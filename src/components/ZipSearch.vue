<template>
  <ion-grid>
    <form v-on:submit.prevent @submit="handle_submit">
      <ion-col>
        <ion-item>
          <ion-label>Code postal:</ion-label>
          <ion-input
            :value="zip"
            @input="zip = $event.target.value"
            placehodler="CP"
            name="zip"
          ></ion-input>
          <ion-select
            :value="origin"
            @ionChange="origin = $event.target.value"
            placeholder="origine"
          >          
            <ion-select-option :key="index" v-for="(region, index) in regions" :value="region">{{ region }}</ion-select-option>
          </ion-select>
        </ion-item>
      </ion-col>
      <ion-col>
        <ion-button type="submit" color="primary" expand="block"
          >Chercher</ion-button
        >
      </ion-col>
    </form>
  </ion-grid>
</template>

<script>
import regions from '../lib/all_regions'

export default {
  name: "ZipSearch",
  data() {
    return {
      zip: "",
      origin: "",
      regions
    };
  },
  methods: {
    handle_submit() {
      this.$emit("get-zip", this.zip, this.origin);
      this.zip = "";
      this.origin = "";
    },
  }

};
</script>