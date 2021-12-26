<template>
  <div id="app">
    <ul>
      <li v-for="(image,index) in images" :key="`image-${index}`">{{images[index]}}
        <button @click="bringToFront(index)">Bring to front</button>
      </li>
      </ul>
    <DraggableContent v-for="(image,index) in images" :key="`image-${index}`"
      ><img :src="image">
    </DraggableContent>
  </div>
</template>

<script>
import DraggableContent from "./components/DraggableContent.vue";

export default {
  name: "App",
  components: {
    DraggableContent,
  },
  data() {
    return {
      images: [
        "https://i.imgur.com/amckVul.jpeg",
        "https://i.imgur.com/9AYsBSU.jpeg",
      ],
    };
  },
  methods:{
    bringToFront(index){
      console.log(index);
      const imgInfo = this.images[index];
      this.images.splice(index,1);
      this.images.push(imgInfo);
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  color: black;
}
img{
  width: 200px;
  height: auto;
}
</style>
