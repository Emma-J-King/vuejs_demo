<script>
import HelloWorld from './components/HelloWorld.vue'
import { defineComponent, ref, onMounted } from 'vue'
import axios from 'axios';
// create get function


export default defineComponent({
  name: 'Test', 
  components: {
    HelloWorld
  },
  setup () {
    let test = ref(null);
    const joke = ref("three");
    
    onMounted(() => {
      axios.get(
        'https://icanhazdadjoke.com/', { //arguments need to be applied 
          responseType: 'json',
          headers: {
            'Accept': 'application/json'
          },
        }
      )
      .then(response => {
        console.log(response.data.joke);
        joke.value = response.data.joke
      })
      .catch(error => {
        console.log(error);
      });
    })
    return {
      test,
      joke
    }
  },
});
// {/* <img 
//           @click="imageChange" 
//           class="smallimg" 
//           :src="imgLoc[index]"
//           > */}
</script>

<!-- <script src="./node_modules/axios/dist/axios.min.js">

</script> -->
<template>
  <header>
    
  </header>

<body>
  <br>
  <br>
  <br>
  <div class="container cc">
      <div class="row c">
        <HelloWorld msg="Do you like jokes?" />
      </div>

      <div class="jrow row c">
        {{ joke }}
      </div>
    </div>
  <div class="containerimage">
    <div class=" row image">
      <br>
      <p> Click for more funny animals</p>
      <img src="../src/images/magdalena-smolnicka-MySy-2bd930-unsplash.jpg" height="300px" width="300px">
      <br>
      Photo by <a href="https://unsplash.com/@magdaleny?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Magdalena Smolnicka</a> on <a href="https://unsplash.com/photos/close-up-photography-of-brown-horse-MySy-2bd930?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
  > </div>
    <div class="row image">
      <br>
      <p> two</p>
      <br>
      <img src="https://hips.hearstapps.com/hmg-prod/images/lionel-animals-to-follow-on-instagram-1568319926.jpg?crop=1.00xw:0.401xh;0,0.282xh&resize=640:*">
    
    </div>
  </div>
</body>
  
  
</template>

<style>

/* .jrow {

border-color: lightslategray;
text-align: center;
display: inline-flex;
} */
.c{
  border-style: solid;
  border-width: thin;
  padding:5px;
  display: flex;
  justify-content: center;
}
.cc {
  border-style: solid;
  border-width: thin;
  border-color: rgb(57, 55, 55) ;
}

.containerimage{
    display: flex;
    flex-direction: row;
    align-items: flex-start
    }

.img {
  width: 100px;
  height: 100px;
}

.p {
  text-align: center;
}
</style>

