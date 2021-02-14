<template>
  <div style="justify-content: unset; width: 100%">
    <ion-header>
      <ion-toolbar>
        <ion-title>INFO CODE POSTAL</ion-title>
      </ion-toolbar>
    </ion-header>        
    <div class="ion-padding">
      <ZipSearch v-on:get-zip="get_zip_info" />
      <div style="width: 100%; display: flex; flex-wrap: wrap;">
      <ZipInfo style="min-width: 33%" :key="index" v-for="(info, index) in infos" v-bind:info="info"/>
</div>
    </div>
  </div>
</template>

<script>
import ZipSearch from "../components/ZipSearch";
import ZipInfo from "../components/ZipInfo";
import regions from '../lib/all_regions'

export default {
  name: "home",
  components: {
    ZipSearch,
    ZipInfo
  },
  
  data() {
    return {
      origins: regions,
      infos: null,
    };
  },
  methods: {
    async get_zip_info(zip, origin) {
      this.infos = null;
      this.infos = [];
      if (!origin) {
        Promise.all(
          this.origins.map((random_origin) => {
            return fetch(`https://api.zippopotam.us/${random_origin}/${zip}`, {
              mode: "cors",
            })
              .then((res) => {
                if (res.status == 200) return res.json();
              })
              .then((data) => {
                if (data) {
                  this.infos = [...this.infos, data];
                }
              });
          })
        ).then(() => {
          if (!this.infos) this.show_alert();
        });
      } else {
        const res = await fetch(`https://api.zippopotam.us/${origin}/${zip}`);
        if (res.status == 404) this.show_alert();
        const info_zip = await res.json();
        this.infos = [...this.infos, info_zip];
      }
    },
    show_alert() {
      return this.$ionic.alertController
        .create({
          header: "Code postal",
          message: "Code postale introuvable",
          buttons: ["OK"],
        })
        .then((alert) => alert.present());
    },
  },
};
</script>
