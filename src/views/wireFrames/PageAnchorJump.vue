<template>
  <v-container>
    <v-row>
      <v-col class="d-none d-sm-block left-menu" sm="2">
        <v-sheet
          :width="width"
          color="rgba(0,0,0,.1)"
          rounded="lg"
          class="fixed pa-2"
          elevation="2"
        >
          <!--  -->
          <v-list height="1000">
            <v-list-subheader>ιηΉθε</v-list-subheader>

            <v-list-item
              v-for="(item, id) in anchorList"
              :key="id"
              :value="item"
              :active="id === currentId"
              active-color="primary"
              rounded="xl"
              @click="jumpToAnchor(item.id)"
            >
              <template v-slot:prepend>
                <v-icon
                  class="d-none d-lg-inline-block"
                  :icon="item.icon"
                ></v-icon>
              </template>

              <v-list-item-title v-text="item.text"></v-list-item-title>
            </v-list-item>
          </v-list>
        </v-sheet>
      </v-col>
      <v-col cols="12" sm="10">
        <v-sheet class="pa-5" min-height="70vh" rounded="lg" elevation="4">
          <template v-for="item in sections" :key="item.index">
            <v-card class="pa-5" :id="item.id" height="2000" color="blue">
              <h1>{{ item.title }}</h1>
            </v-card>
            <v-divider class="my-5"></v-divider>
          </template>
        </v-sheet>
      </v-col>
    </v-row>
    <div class="to-top">
      <v-card width="100" height="200" color="rgba(0,0,0,.3)">
        <v-btn
          @click="backToTop()"
          class="ma-2"
          color="indigo"
          icon="mdi-arrow-up-bold"
        ></v-btn>
      </v-card>
    </div>
  </v-container>
</template>

<script setup lang="ts">
import { useDisplay } from "vuetify";

import { useWindowScroll } from "@vueuse/core";
const { name } = useDisplay();

const currentId = ref("images");

const width = computed(() => {
  // name is reactive and
  // must use .value
  switch (name.value) {
    case "md":
      return 125;
    case "lg":
      return 175;
    case "xl":
      return 275;
    case "xxl":
      return 375;
  }
  console.log(name.value);
  return undefined;
});

const jumpToAnchor = (id) => {
  let element = document.getElementById(id);
  element.scrollIntoView({ behavior: "smooth" });
};

const backToTop = () => {
  y.value = 0;
};

const anchorList = ref([
  { text: "ι«ζΈεΎεΊ", icon: "mdi-clock", id: "images" },
  { text: "θ?Ύθ?‘ζη¨", icon: "mdi-account", id: "lessons" },
  { text: "ηι’θ?Ύθ?‘", icon: "mdi-flag", id: "design" },
]);

const sections = ref([
  { title: "ι«ζΈεΎεΊ", id: "images" },
  { title: "θ?Ύθ?‘ζη¨", id: "lessons" },
  { title: "ηι’θ?Ύθ?‘", id: "design" },
]);

const { x, y } = useWindowScroll();

// δ½Ώη¨xεyειθ·εε½ει‘΅ι’ηζ¨ͺεεηΊ΅εζ»ε¨δ½η½?
console.log(x, y);
</script>

<style>
.fixed {
  position: fixed;
  top: 40px;
}

.to-top {
  position: fixed;
  right: 0;
  bottom: 100px;
}
</style>
