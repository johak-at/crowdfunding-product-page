<script setup>
import { Icon } from "@iconify/vue";
import { Camera, CameraResultType } from "@capacitor/camera";
import { useStore } from "~/store/store";
import { storeToRefs } from "pinia";

// useStore() and name handling:
const store = useStore();
const name = storeToRefs(store).name;

const newName = ref("");
function setName() {
  store.name = newName.value;
  newName.value = "";
}

// taking a picture and displaying it:
const imageUrl = ref(null);
async function takePic() {
  const image = await Camera.getPhoto({
    quality: 90,
    allowEditing: true,
    resultType: CameraResultType.Uri,
  });
  imageUrl.value = image.webPath;
}

definePageMeta({
  alias: "/home",
});

let backed_amount = ref(89914);
let backers = ref(5007);

function addDonation() {
  if (
    !isNaN(donation_amount.value) &&
    donation_amount.value != "" &&
    donation_amount.value != null &&
    donation_amount.value != undefined &&
    donation_amount.value >= 1 &&
    donation_amount.value <= 100000
  ) {
    backed_amount.value += parseInt(donation_amount.value);
    backers.value++;
  } else {
    alert("Zwischen 1 und 100000 du Hund!");
  }
}
//make a function that sets backed amount as a format with 1000 seperator
</script>

<template>
  <!--<div class="Image">
    <img src="@/public/image-hero-desktop.jpg" alt="Desktop">
</div>-->

  <!--Eigenes Div für die ganze Seite-->
  <div class="Seite">
    <div class="Header">
      <a class="Header-title" href="http://localhost:3000/">Crowdfunding</a>
      <div class="rightside">
        <a
          class="Header-Insta"
          target="_blank"
          href="https://www.instagram.com/johak.pongau/"
          >Insta</a
        >
        <a class="Header-about" href="http://localhost:3000/about">About</a>
      </div>
    </div>

    <!-- Put this part before </body> tag -->
    <input type="checkbox" id="my-modal" class="modal-toggle" />
    <div class="modal">
      <div class="modal-box">
        <h3 class="font-bold text-lg">Back this Project</h3>
        <h4 class="modal_untertitel">
          Want to support us in bringing Schnecken Checker out in the world?
        </h4>
        <input
          id="donation_amount"
          type="number"
          placeholder="Donation Amount"
          class="input w-full max-w-xs text-[#f1f1f1] mt-10"
          min="1"
          max="100000"
        />
        <p class="py-4"></p>
        <div class="modal-action">
          <label for="my-modal" class="btn" @click="addDonation">Donate!</label>
        </div>
      </div>
    </div>
    <div class="cards-middle">
      <!--------------------------------------------------------------------------------->

      <div class="top-card-section">
        <div class="logo">
          <img src="logo-mastercraft.svg" alt="Logo" class="base-logo" />
        </div>
        <h1 class="top-title">Schnecken Checker</h1>
        <h2 class="top-subtitle">
          Der beste Männer- und Frauenmagnet ALLERZEITEN!
        </h2>
        <div class="top-buttons">
          <label for="my-modal" class="btn btn-accent">
            Back this project
          </label>
          <button class="btn btn-accent">Bookmarked</button>
        </div>
      </div>
      <div class="middle-card-section">
        <div class="middle_amounts">
          <div class="moneyamount">
            <h1>${{ backed_amount }}</h1>
            <h2 class="money_subtitle">of $ 100,000</h2>
          </div>
          <div class="backers">
            <h1>{{ backers }}</h1>
            <h2 class="money_subtitle">total backers</h2>
          </div>
          <div class="days">
            <h1>56</h1>
            <h2 class="money_subtitle">days left</h2>
          </div>
        </div>
      </div>
      <div class="bottom-card-section">
        <div class="product-1"></div>
        <div class="product-2"></div>
      </div>
    </div>
  </div>
</template>

<style>
.modal {
  color: black;
}

.modal-box {
  background-color: white;
  height: 800px;
  width: 750px;
}

.modal_untertitel {
  color: grey;
  font-size: 14px;
}

.days {
  color: black;
  font-size: 30px;
  font-weight: bold;
  margin-left: 70px;
  max-width: 250px;
  max-height: 200px;
  margin-top: 60px;
  margin-right: 70px;
}

.backers {
  color: black;
  font-size: 30px;
  font-weight: bold;
  margin-left: 70px;
  max-width: 250px;
  max-height: 200px;
  margin-top: 60px;
}

.money_subtitle {
  color: grey;
  font-size: 18px;
  font-weight: lighter;
}

.moneyamount {
  color: black;
  font-size: 30px;
  font-weight: bold;
  margin-left: 70px;
  margin-top: 60px;
  max-width: 250px;
  max-height: 200px;
}

.top-buttons {
  display: flex;
  justify-content: space-around;
  margin-top: 30px;
}

.top-title {
  color: black;
  font-size: 25px;
  font-weight: bold;
  text-align: center;
}
.top-subtitle {
  color: grey;
  font-size: 16px;
  text-align: center;
}

.logo {
  width: 50px;
  height: 50px;
  margin-top: -25px;
  margin-left: 350px;
}

.top-card-section {
  width: 750px;
  height: 200px;
  border-radius: 10px;
  /*center vertically without using margin*/
  margin-top: 30px;
  margin-left: 25px;
  border-width: 0.5px;
  border-style: solid;
  /*border-color: grey;*/
  background-color: white;
}
.middle_amounts {
  display: flex;
  justify-content: space-between;
}
.middle-card-section {
  width: 750px;
  height: 200px;
  border-radius: 10px;
  margin-top: 20px;
  margin-left: 25px;
  border-width: 0.5px;
  border-style: solid;
  /* border-color: grey;*/
  background-color: white;
}
.bottom-card-section {
  width: 750px;
  height: 450px;
  border-radius: 10px;
  margin-top: 20px;
  margin-left: 25px;
}
.product-1 {
  width: 750px;
  height: 215px;
  border-radius: 10px;
  border-width: 0.5px;
  border-style: solid;
  /**border-color: grey;*/
  background-color: white;
}
.product-2 {
  width: 750px;
  height: 215px;
  border-radius: 10px;
  margin-top: 20px;
  border-width: 0.5px;
  border-style: solid;
  /* border-color: grey;*/
  background-color: white;
}

.Header {
  display: flex;
  justify-content: space-between;
  margin-top: 3px;
}
.rightside {
  display: flex;
  justify-content: adjust;
  margin-top: 3px;
}

.cards-middle {
  width: 800px;
  height: 100vh;
  /**center horizontally */
  margin: 0 auto;
}

.Header-about {
  color: black;
  font-size: 16px;
  font-weight: bold;
  margin-left: 50px;
  margin-right: 100px;
}

.Header-title {
  color: black;
  font-size: 20px;
  font-weight: bold;
  margin: 0;
  padding: 0;
  margin-left: 100px;
}
.Header-Insta {
  color: black;
  font-size: 16px;
  font-weight: 70;
  font-weight: bold;
}
div {
}

.v-main {
  background-color: #f9f9f9;
  overflow: hidden;
  max-width: 100vw;
  max-height: 100vh;
}
</style>
