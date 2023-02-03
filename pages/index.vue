<script setup>
import { Icon } from "@iconify/vue";
import { Camera, CameraResultType } from "@capacitor/camera";
import { useStore } from "~/store/store";
import { storeToRefs } from "pinia";

// Zwei Objekte mit den Eigenschaften Title, Url, Price, Description und Left. Left gibt an wie viele von dem jeweiligen Reward noch verfügbar sind.
const rewards = ref([
  {
    id: 1,
    title: "2er Bmw",
    url: "/bmw2er.jpg",
    price: 100,
    description: "Ein getunter 2er BMW mit 500 PS und 1000 NM Drehmoment",
    left: 100,
    favorite: true,
  },
  {
    id: 2,
    title: "4er Bmw",
    url: "/bmw4er.jpg",
    price: 200,
    description: "Ein getunter 4er BMW mit 900 PS und 1200 NM Drehmoment",
    left: 80,
    favorite: false,
  },
]);

function toggle() {
  // set the value to the opposite
  console.log(rewards[0].favorite);
}

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

let backed_amount = ref(57000);
let backers = ref(5007);

// Überprüft, ob der Eingegebene Betrag in den richtigen Bereich liegt, wenn ja wird der Betrag dem Gesamtbetrag hinzugefügt und die Anzahl der Spender um 1 erhöht.
// Wenn der Betrag nicht in den richtigen Bereich liegt, wird eine Fehlermeldung ausgegeben.
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
    ClearFields();
  } else if (donation_amount.value == "" || donation_amount.value == null) {
  } else {
    alert("Zwischen 1 und 100000 du");
  }
}
function addDonation1() {
  if (
    !isNaN(donation_amount1.value) &&
    donation_amount1.value != "" &&
    donation_amount1.value != null &&
    donation_amount1.value != undefined &&
    donation_amount1.value >= 100 &&
    donation_amount1.value <= 100000
  ) {
    backed_amount.value += parseInt(donation_amount1.value);
    backers.value++;
    ClearFields();
    rewards.value[0].left -= 1;
  } else if (donation_amount1.value == "" || donation_amount1.value == null) {
  } else {
    alert("Zwischen 100 und 100000 du");
  }
}
function addDonation2() {
  if (
    !isNaN(donation_amount2.value) &&
    donation_amount2.value != "" &&
    donation_amount2.value != null &&
    donation_amount2.value != undefined &&
    donation_amount2.value >= 200 &&
    donation_amount2.value <= 100000
  ) {
    backed_amount.value += parseInt(donation_amount2.value);
    backers.value++;
    ClearFields();
    rewards.value[1].left -= 1;
  } else if (donation_amount2.value == "" || donation_amount2.value == null) {
  } else {
    alert("Zwischen 100 und 100000 du");
  }
}
// macht den Input Feld leer
function ClearFields() {
  donation_amount.value = "";
  donation_amount1.value = "";
  donation_amount2.value = "";
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

    <input type="checkbox" id="my-modal-fav" class="modal-toggle" />
    <div class="modal">
      <div class="modal-box">
        <label for="my-modal-fav" class="modal-close">X</label>
        <h3 class="font-bold text-lg">Favorites</h3>
        <h4 class="modal_untertitel">
          These are your favorite projects. You can remove them from your
          favorites
        </h4>
        <!-- create a list of the favorite rewards using v-if and v-for -->

        <div
          v-for="reward in rewards"
          flex
          flex-col
          items-center
          class="text-xl mt-60px"
        >
          <!-- create an x to remove from favorites -->

          <li v-if="reward.favorite">
            {{ reward.title }} - {{ reward.left }} left &bs
            <button class="ml-10px" @click="reward.favorite = false">X</button>
          </li>
        </div>

        <div class="modal-items"></div>
        <p class="py-4"></p>
        <div class="modal-action"></div>
      </div>
    </div>

    <!-- Put this part before </body> tag -->
    <input type="checkbox" id="my-modal" class="modal-toggle" />
    <div class="modal">
      <div class="modal-box">
        <!--create a X to close modal-->
        <label for="my-modal" class="modal-close">X</label>

        <h3 class="font-bold text-lg">Back this Project</h3>
        <h4 class="modal_untertitel">
          Want to support us in bringing Schnecken Checker out in the world?
        </h4>
        <!-- grey out whole div if radio button not selected -->

        <div class="modal-Items">
          <div class="collapse mt-49px bg-white border-1 border-grey">
            <input type="checkbox" />
            <div class="collapse-title text-l font-medium">
              Pledge with no reward
            </div>
            <div class="collapse-content">
              <p>Help us out with any amount to donate!</p>
              <input
                id="donation_amount"
                type="number"
                placeholder="Donation Amount"
                class="h-30px w-150px border-1 border-grey"
                min="1"
                max="100000"
              />
              <label
                for="my-modal"
                class="btn btn-accent btn-modal ml-320px"
                @click="addDonation()"
                >Donate!</label
              >
            </div>
          </div>

          <div class="collapse mt-49px border-1 border-grey bg-white">
            <input type="checkbox" />
            <div class="collapse-title text-l font-medium">
              {{ rewards[0].title }}
            </div>
            <div class="collapse-content">
              <p>
                <span class="text-[black]">{{ rewards[0].left }} left</span>
              </p>
              <p class="mt-3px">{{ rewards[0].description }}</p>
              <input
                id="donation_amount1"
                type="number"
                placeholder="Donation Amount"
                class="h-30px w-150px border-1 border-grey"
                min="100"
                max="100000"
              />
              <label
                for="my-modal"
                class="btn btn-accent btn-modal ml-320px"
                @click="addDonation1()"
                >Donate!</label
              >
            </div>
          </div>
          <div class="collapse mt-49px border-1 border-grey bg-white">
            <input type="checkbox" />
            <div class="collapse-title text-l font-medium">
              {{ rewards[1].title }}
            </div>
            <div class="collapse-content">
              <p>
                <span class="text-[black]">{{ rewards[1].left }} left</span>
              </p>
              <p class="mt-3px">{{ rewards[1].description }}</p>
              <input
                id="donation_amount2"
                type="number"
                placeholder="Donation Amount"
                class="h-30px w-150px border-1 border-grey"
                min="200"
                max="100000"
              />
              <label
                for="my-modal"
                class="btn btn-accent btn-modal ml-320px"
                @click="addDonation2()"
                >Donate!</label
              >
            </div>
          </div>
        </div>
        <p class="py-4"></p>
        <div class="modal-action"></div>
      </div>
    </div>
    <div class="cards-middle">
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
          <label for="my-modal-fav" class="btn btn-accent"> Favorites </label>
        </div>
      </div>
      <div class="middle-card-section flex flex-col">
        <div class="middle_amounts">
          <div class="moneyamount">
            <!-- wenn der Betrag >= 100000 dann wird die Klasse text-success hinzugefügt und damit wird der Text grün angezeigt -->
            <h1 :class="{ 'text-success': backed_amount >= 100000 }">
              ${{ backed_amount }}
            </h1>
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
        <!-- Progress Bar mit der Klasse progress-success wenn die backed_amount >= 100000 ist dann wird der Balken voll und grün angezeigt. -->
        <progress
          class="progress w-11/12 m-auto"
          :class="{ 'progress-success': backed_amount >= 100000 }"
          :value="backed_amount"
          max="100000"
        ></progress>
        <!---------------------------------------------------------------------- -->
      </div>
      <div class="bottom-card-section text-black">
        <!-- Aus der rewards Objekt werden die Daten ausgelesen und in die Karten gelegt und die Bilder werden aus dem Array gezogen und angezeigt. -->
        <div
          v-for="(reward, index) in rewards"
          :key="rewards.id"
          flex
          flex-col
          items-center
        >
          <div class="w-12/12 flex justify-between">
            <h1>{{ reward.title }}</h1>
            <p>Pledge {{ reward.price }} $ or more</p>
          </div>
          <img :src="reward.url" alt="a picture of a car" class="carPics" />
          <div>{{ reward.description }}</div>
          <div
            @click="rewards[index].favorite = !rewards[index].favorite"
            class="favorite"
          >
            <Icon
              v-if="!reward.favorite"
              text-8
              icon="ic:baseline-star-outline"
            />
            <Icon
              v-else
              text-8
              icon="ic:outline-star"
              @click="clicked = false"
            />
          </div>
          <div class="w-12/12 flex justify-between mb-30px mt-0">
            {{ reward.left }} left
            <!-- ---------------------------------------------------------------------- -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
/* make the Header-button work */

.favorite {
  position: relative;
  cursor: pointer;
  margin-left: 700px;
  margin-top: -25px;
}

.radio-btn {
  margin-right: 10px;
  margin-left: 10px;
}
.modal-Items-top {
  width: 460px;
  height: 100px;
  border-radius: 10px;
  border-width: 0.5px;
  border-style: solid;
  border-color: grey;
  background-color: white;
  margin-top: 20px;
  display: flex;
  justify-content: left;
}

.modal-Items-middle {
  width: 460px;
  height: 100px;
  border-radius: 10px;
  border-width: 0.5px;
  border-style: solid;
  border-color: grey;
  background-color: white;
  margin-top: 20px;
  display: flex;
  justify-content: left;
}

.modal-Items-bottom {
  width: 460px;
  height: 100px;
  border-radius: 10px;
  border-width: 0.5px;
  border-style: solid;
  border-color: grey;
  background-color: white;
  margin-top: 20px;
  display: flex;
  justify-content: left;
}

.modal-close {
  position: absolute;
  font-weight: bold;
  top: 0;
  right: 0;
  padding: 1rem;
  cursor: pointer;
  z-index: 100;
}
.carPics {
  width: 750px;
  height: 400px;
  border-radius: 10px;
  border-width: 0.5px;
  border-style: solid;
  /**border-color: grey;*/
  background-color: white;
}

.modal {
  color: black;
}

.modal-box {
  background-color: #f1f1f1;
  height: 600px;
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
  /*max-width: 100vw;
  max-height: 100vh;*/
}
.hydrated {
  background-color: #f9f9f9;
}
</style>
