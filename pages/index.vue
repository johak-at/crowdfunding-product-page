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
</script>

<template>
  
<!--<div class="Image">
    <img src="@/public/image-hero-desktop.jpg" alt="Desktop">
</div>-->

<!--Eigenes Div für die ganze Seite-->
<div class="Seite">
    <div class="Header">
      <a class="Header-title">Crowdfunding</a>
      <div class="rightside">
      <a class="Header-Insta">Insta</a>
      <a class="Header-about">About</a>
      </div>
      
  </div>
  <div class="cards-middle">
    
    
    <div class="top-card-section">
      <div class="logo"><img src="logo-mastercraft.svg" alt="Logo" class="base-logo"></div>
      <h1 class="top-title">Schnecken Checker</h1>
      <h2 class="top-subtitle">Das beste Männer- und Frauenmagnet ALLERZEITEN!</h2>
      <div class="top-buttons">
        <button class="btn btn-accent mx-30">Back this project</button>
        <button class="btn btn-accent mx-30">Bookmarked</button>
      </div>

    </div>
    <div class="middle-card-section"></div>
    <div class="bottom-card-section">
      <div class="product-1"></div>
      <div class="product-2"></div>
    </div>


  </div>
  
</div>
    

    
</template>

<style>

.top-buttons{
  display: flex;
  justify-content: space-between;
  margin-top: 50px;
}

.top-title{
  color: black;
  font-size: 25px;
  font-weight: bold;
  text-align: center;

}
.top-subtitle{
  color: grey;
  font-size: 16px;
  text-align: center;

}

.logo{
  width: 50px;
  height: 50px;
  margin-top: -25px;
  margin-left: 350px;
}

.top-card-section{
  width: 750px;
  height: 250px;
  border-radius: 10px;
  /*center vertically without using margin*/
  margin-top: 30px;
  margin-left: 25px;
  border-width: 0.5px;
 border-style:solid;
 border-color:grey;



}
.middle-card-section{
  width: 750px;
  height: 200px;
  border-radius: 10px;
  margin-top: 30px;
  margin-left: 25px;
  border-width: 0.5px;
 border-style:solid;
 border-color:grey;

}
.bottom-card-section{
  width: 750px;
  height: 450px;
  border-radius: 10px;
  margin-top: 30px;
  margin-left: 25px;

}
.product-1{
  width: 750px;
  height: 215px;
  border-radius: 10px;
  border-color:grey;
  border-width: 0.5px;
 border-style:solid;
 border-color:grey;

}
.product-2{
  width: 750px;
  height: 215px;
  border-radius: 10px;
  margin-top: 20px;
  border-color:grey;
  border-width: 0.5px;
 border-style:solid;
 border-color:grey;

}

.Header{
  display: flex;
  justify-content: space-between;
}
.rightside{
  display: flex;
  justify-content: adjust;
  margin-top: 3px;
}

.cards-middle{
  width: 800px;
  height: 100vh;
  /**center horizontally */
  margin: 0 auto;
  

}

.Header-about{
  color:black;
  font-size: 16px;
  font-weight: bold; 
  margin-left: 50px;
  margin-right: 100px;
}

.Header-title{
        color:black;
        font-size: 20px;
        font-weight: bold; 
        margin: 0;
        padding: 0;
        margin-left: 100px;
    }
.Header-Insta{
        color:black;
        font-size: 16px;
        font-weight: 70; 
        font-weight: bold;

    }
div{
}

    .v-main{
      background-color: white;
    }
</style>
