<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>ZipCode</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ZipSearch @get-zip="getZipInfo"/>
      <ZipInfo :info="info" @clear-zipinfo="clearZipInfo"/>
    </ion-content>
  </div>
</template>

<script>
import ZipSearch from "../components/ZipSearch";
import ZipInfo from "../components/ZipInfo";
export default {
  name: "home",
  components: { ZipSearch, ZipInfo },
  data() {
    return {
      info: null
    };
  },
  methods: {
    async getZipInfo(zip) {
      const res = await fetch(`https://api.zippopotam.us/us/${zip}`);
      if (res.status == 404) {
        this.showAlert();
      } else {
        this.info = await res.json();
      }
    },
    showAlert() {
      return this.$ionic.alertController
        .create({
          header: "Enter Zipcode",
          message: "Please enter a valid US Zipcode",
          buttons: ["OK"]
        })
        .then(a => a.present());
    },
    clearZipInfo() {
      this.info = null;
    }
  }
};
</script>
