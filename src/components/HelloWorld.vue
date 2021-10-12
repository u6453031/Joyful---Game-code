<template>

  <n-grid :x-gap="12" :y-gap="8" style="padding:30px 0px 0px 0px;">
    <n-gi x-gap="12" :span="6" :offset="2">
      <a style="font-size: 140%; padding: 20px; font-weight: bold">Joyful Fashionista</a>
      <NButton @click="changeBack">Change Background</NButton>
      <div style="position: relative;padding:30px 0px 0px 0px;" @dragover.prevent="over" @drop.prevent="drop">
        <div :style="{ 'background-image': 'url(' + birdproject.background[birdproject.backshow] + ')', 'background-size': '100%', width: '100%', position: 'absolute' }">
          <img :src=birdproject.bird style="width:100%; padding:100px 0px 0px 0px;" />
        </div>
                <div style="position:absolute;width: '100%'">
                  <img :src="birdproject.shoes[birdproject.shoesShow]" style="width:100%;padding:100px 0px 0px 0px;" />
                </div>
        <div style="position:absolute;width: '100%'">
          <img :src="birdproject.hat[birdproject.hatShow]" style="width:100%;padding:100px 0px 0px 0px;" />
        </div>
        <div style="position:absolute;width: '100%'">
          <img :src="birdproject.body[birdproject.bodyShow]" style="width:100%;padding:100px 0px 0px 0px;" />
        </div>

      </div>
    </n-gi>
    <n-gi :span="16">
      <n-space>
        <span style="font-size: 200%;">Hats</span>
      </n-space>
      <n-space>
        <img v-for="(items, i) in birdproject.hat" v-bind:key="items" :src="items" width="100" border="2" draggable @dragstart="start('hats', i)" />
      </n-space>
      <n-space>
        <span style="font-size: 200%;">Body</span>
      </n-space>
      <n-space>
        <img v-for="(items, i) in birdproject.body" v-bind:key="items" :src="items" width="100" border="2" draggable @dragstart="start('body', i)" />
      </n-space>
      <n-space>
        <span style="font-size: 200%;">Shoes</span>
      </n-space>
      <n-space>
        <img v-for="(items, i) in birdproject.shoes" v-bind:key="items" :src="items" width="100" border="2"  draggable @dragstart="start('shoes', i)" />
      </n-space>
    </n-gi>
  </n-grid>


</template>
<script>
import { defineComponent, reactive } from 'vue';
import { NGrid, NGi, NButton, NSpace } from 'naive-ui';

export default defineComponent({
  components: {
    NGrid,
    NGi,
    NButton,
    NSpace,
  },
  setup() {
    var birdproject = reactive({
      background: ['./back/1.jpg', './back/2.jpg', './back/3.jpg', './back/4.jpg', './back/5.jpg', './back/6.jpg', './back/7.jpg', './back/8.jpg', './back/9.jpg', './back/10.jpg', './back/11.jpg', './back/12.jpg', './back/13.jpg', './back/14.jpg'],
      hat: ['./layers/hats/1.png', './layers/hats/2.png', './layers/hats/3.png', './layers/hats/4.png', './layers/hats/5.png', './layers/hats/6.png', './layers/hats/7.png', ''],
      body: ['./layers/body/1.png', './layers/body/2.png', './layers/body/3.png', './layers/body/4.png','./layers/flowers.png','./layers/body/5.png', './la' +
      'yers/body/6.png', ''],
      shoes: ['./layers/shoes/1.png', './layers/shoes/2.png', './layers/shoes/3.png', './layers/shoes/4.png', './layers/shoes/5.png', './layers/shoes/6.png', './layers/shoes/7.png', ''],
      bird:"./layers/bird.png",
      backshow: 0,
      hatShow: 7,
      shoesShow: 7,
      bodyShow: 7,
      Transitem: 0,
      Transtype: '',
    });
    const start = (type, i) => {
      birdproject.Transitem = i;
      birdproject.Transtype = type;
    };
    const drop = () => {
      if (birdproject.Transtype == 'hats') {
        birdproject.hatShow = birdproject.Transitem;
      } else if (birdproject.Transtype == 'body') {
        birdproject.bodyShow = birdproject.Transitem;
      } else {
        birdproject.shoesShow = birdproject.Transitem;
      }
    };
    const changeBack = () => {
      birdproject.backshow = getRandomIntInclusive(0, 13);
    };

    const getRandomIntInclusive = (min, max) => {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min + 1)) + min;
    };

    return {
      birdproject,
      changeBack,
      start,
      drop,
    };
  },
});
</script>

<style></style>
