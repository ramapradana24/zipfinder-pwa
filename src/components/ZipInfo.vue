<template>
  <div v-if="info">
    <ion-card>
      <ion-card-header>
        <ion-card-subtitle>{{ info['post code'] }}</ion-card-subtitle>
        <ion-card-title>{{ info['places'][0]['place name'] }}</ion-card-title>
      </ion-card-header>
      <ion-card-content>
        <ion-list>
          <ion-item>
            <ion-label>
              <strong>State:</strong>
              {{ info['places'][0]['state'] }} {{ info['places'][0]['state abbreviation'] }}
            </ion-label>
          </ion-item>
        </ion-list>
      </ion-card-content>
    </ion-card>
    <ion-button color="light" expand="block" @click="clearZipInfo">Clear</ion-button>
  </div>
</template>

<script>
export default {
  name: "ZipInfo",
  props: ["info"],
  methods: {
    clearZipInfo() {
      this.$emit("clear-zipinfo", null);
    }
  }
};
</script>