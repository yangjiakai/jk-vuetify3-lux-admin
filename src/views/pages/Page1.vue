<template>
  <v-container>
    <v-row>
      <v-col class="d-none d-sm-block" sm="2">
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
              v-for="item in categoryList"
              :key="item.category_id"
              :value="item"
              active-color="primary"
              rounded="xl"
              @click="jumpToAnchor(`category_${item.category_id}`)"
            >
              <template v-slot:prepend>
                <v-icon start icon="mdi-cloud-upload"></v-icon>
              </template>

              <v-list-item-title
                v-text="item.category_name_cn"
              ></v-list-item-title>
            </v-list-item>
          </v-list>
        </v-sheet>
      </v-col>
      <v-col cols="12" sm="10">
        <v-sheet class="pa-5" min-height="70vh" rounded="lg" elevation="4">
          <template
            v-for="sitesSection in siteList"
            :key="sitesSection.category_id"
          >
            <v-sheet
              style="border: 1px solid #ccc; border-radius: 1rem"
              class="pa-5 mb-5"
              height=""
              color=""
            >
              <h1 :id="`category_${sitesSection.category_id}`" class="text-h6">
                {{ sitesSection.category_name_cn }}
              </h1>
              <v-divider class="my-5"></v-divider>
              <v-row>
                <v-col
                  xs="12"
                  sm="6"
                  lg="3"
                  xl="2"
                  v-for="site in sitesSection.sites"
                  :key="site.site_id"
                >
                  <v-hover v-slot="{ isHovering, props }">
                    <a :href="site.href" target="_blank">
                      <v-card
                        height="120"
                        v-bind="props"
                        :elevation="isHovering ? 6 : 2"
                      >
                        <v-card-title
                          class="text-subtitle-1 d-flex align-center"
                        >
                          <span class="mr-2">
                            <v-img
                              :src="site.icon"
                              width="20"
                              aspect-ratio="1"
                            ></v-img
                          ></span>
                          <span class="text-truncate">{{
                            site.site_name
                          }}</span>
                        </v-card-title>
                        <!-- <v-card-subtitle>{{ site.description}}</v-card-subtitle> -->
                        <v-card-text>
                          <p class="two-line">
                            {{ site.description }}
                          </p>
                        </v-card-text>
                      </v-card>
                    </a>
                  </v-hover>
                </v-col>
              </v-row>
            </v-sheet>
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
import sitesData from "@data/sites.json";
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

watch(
  () => name.value,
  (newVal) => {}
);

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

// const jsonData = reactive({}); // ε­ε¨jsonζ°ζ?
const sites = ref([]); // ε­ε¨jsonζ°ζ?

onMounted(() => {
  sites.value = sitesData.sites;
});

const categoryList = computed(() => {
  return uniqueArray(
    sites.value.map((item) => {
      return {
        category_id: item.category_id,
        category_name: item.category_name,
        category_name_cn: item.category_name_cn,
      };
    }),
    "category_id"
  );
});

const siteList = computed(() => {
  let sitesObject = groupByKey(sites.value, "category_id");

  let list = [];
  for (const key in sitesObject) {
    const value = sitesObject[key];
    list.push({
      category_id: key,
      category_name_cn: value[0].category_name_cn,
      sites: value,
    });
  }

  return list;
});

// εε»ΊδΈδΈͺεͺεε«ε―δΈ id εΌηε―Ήθ±‘ηζ°ζ°η»
let uniqueArray = (objectArr, key) => {
  // ε©η¨ map ε Set ε―Ήθ±‘ε?η°ε―Ήθ±‘ζ°η»ηε»ι
  return [...new Set(objectArr.map((item) => item[key]))].map((id) => {
    return objectArr.find((item) => item[key] === id);
  });
};

// ε―Ήθ±‘ζ°η»ιθΏι?εθΏθ‘εη»
let groupArray = (objects, key) => {
  var groups = objects.reduce((result, item) => {
    if (result[item[key]]) {
      result[item[key]].push(item);
    } else {
      result[item[key]] = [item];
    }
    return result;
  }, {});

  return groups;
};

const groupByKey = (objects, key) => {
  let groupData = objects.reduce((acc, obj) => {
    if (!acc[obj[key]]) {
      acc[obj[key]] = [];
    }
    acc[obj[key]].push(obj);
    return acc;
  }, {});

  return groupData;
};

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

a {
  text-decoration: none;
}

.two-line {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
}
</style>
