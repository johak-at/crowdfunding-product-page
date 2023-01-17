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
  <template>

<div class="Image">
    <img src="@/public/image-hero-desktop.jpg" alt="Desktop">
</div>


    <h1 class="title">ASD</h1>

    
</template>
</template>

<style>
title{
        
        background-color:black

        

        
    }


    main{
        background-color: white;
        margin-left: 471.5px;
        margin-right: 471.5px;
    }
</style>
