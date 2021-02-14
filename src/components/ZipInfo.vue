<template>
  <div>
    <ion-card v-if="info">
      <ion-card-header>
        <ion-card-title>{{ info["post code"] }}</ion-card-title>
        <ion-card-subtitle>{{
          info["places"][0]["place name"]
        }}</ion-card-subtitle>
      </ion-card-header>
      <ion-card-content>
        <ion-list>
          <ion-item>
            <span style="padding-right: 0.2rem">Etat:</span>
            <strong>
              {{ info["places"][0].state }}
            </strong>
          </ion-item>
          <ion-item>
            <span style="padding-right: 0.2rem">Pays:</span>
            <strong>
              {{ info.country }}
            </strong>
          </ion-item>
          <ion-item>
            <span style="padding-right: 0.2rem">Abbréviation:</span>
            <strong>
              {{ info["country abbreviation"] }}
            </strong>
          </ion-item>
        </ion-list>
      </ion-card-content>
    </ion-card>
  </div>
</template>

<script>
export default {
  name: "ZipInfo",
  props: ["info"],
};
</script>