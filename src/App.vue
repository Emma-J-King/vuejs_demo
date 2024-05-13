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
    //create onclick image array
    // replace images within the array
    const imgLoc = ref([
      "https://images.pexels.com/photos/1670413/pexels-photo-1670413.jpeg?cs=srgb&dl=pexels-prasanthdas-1670413.jpg&fm=jpg",
      "https://t4.ftcdn.net/jpg/01/66/10/03/360_F_166100342_KbTGIRrnrlwGDZSXSMpH3zfn2dxyTKae.jpg",
      "https://cdn.pixabay.com/photo/2024/04/18/19/14/monkey-8704855_1280.jpg",
      "https://images.rawpixel.com/image_png_social_square/cHJpdmF0ZS9sci9pbWFnZXMvd2Vic2l0ZS8yMDIzLTA3L3JvYl9yYXdwaXhlbF9waG90b2dyYXBoX29mX2FfYmFieV9vcmFndXRhbl9pc29sYXRlZF9vbl93aGl0ZV9zdF84ZTE2OTRmZi1lOWU2LTQ0MTEtYWQzNC00NTdjOGE4NjBhNzYtNXgtaHEtc2NhbGUtNV8wMHgtam9iMTg5NF8xLnBuZw.png",
      "https://images.freeimages.com/images/large-previews/497/uluwatu-monkey-1376207.jpg?fmt=webp&w=500",
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQWBDue7ImdDCVK1_wHPP1U2Tnmy6HXn5XOURixHNabKg&s"
    ]);

    const index = ref(0);
    const imageChange = function () {
      // increment index
      index.value ++
      // catch too high a number
      if (index.value === imgLoc.value.length){
        index.value = 0
      }
    };
    
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
      joke,
      // add onclick (image location, imagechange and index)
      imgLoc,
      imageChange,
      index
    }
  },
});

</script>

<!-- <script src="./node_modules/axios/dist/axios.min.js">

</script> -->
<template>
  <header>
    Workplace breather
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
      <img 
      @click="imageChange" 
      height="300px" width="300px" 
      :src="imgLoc[index]"
    >

     

    </div>
    <div class="row image">
      <br>
      <p> Or we can click for you here</p>
      <img src="https://hips.hearstapps.com/hmg-prod/images/lionel-animals-to-follow-on-instagram-1568319926.jpg?" height="300px" width="300px">
      <br>
      Picture courtesy of Good Housekeeping
    
    </div>
  </div>
  
</body>
    
  
</template>

<style>

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
    align-items: flex-start;
    
    }

.img {
  width: 100px;
  height: 100px;
  
}

.p {
  text-align: center;
}

.image {
margin: 150px;
}

.smallimg {
  height:300px;

} 
</style>

