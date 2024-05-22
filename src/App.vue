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
    const images = ref([
      {
        "loc": "https://images.unsplash.com/photo-1551884831-bbf3cdc6469e?q=80&w=1948&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        "photographerCredit": "Magdalena Smolnicka"
      },

      {
        "loc": "https://media.istockphoto.com/id/1266736164/photo/playful-pup-on-the-bed.jpg?s=2048x2048&w=is&k=20&c=Re6-pVxU4UEjYiS5255-df1sQfmJrCBX-u6x0DArCEA=",
        "photographerCredit": "SolStock"
      },

      {
        "loc": "https://images.unsplash.com/photo-1526336024174-e58f5cdd8e13?q=80&w=1948&auto=format&fit",
        "photographerCredit": "Karina Vorozheeva"
      },

      {
        "loc": "https://static.euronews.com/articles/stories/04/97/98/10/828x1242_cmsv2_792920c6-ff80-54db-b713-54fbbf7a1062-4979810.jpg",
        "photographerCredit": "Brigitte Alcalay Marcon"
      },

      {
        "loc":"https://hips.hearstapps.com/hmg-prod/images/lionel-animals-to-follow-on-instagram-1568319926.jpg?",
        "photographerCredit": "Picture courtesy of Good Housekeeping"
      },
    ]);
    

     const index = ref(0);
     const imageLeft = function () {
      // increment index
      index.value ++
      // catch too high a number
      if (index.value === images.value.length){
        index.value = 0
      }
    };
   

    const images2 =ref([
      {
        "loc":"https://media.istockphoto.com/id/1402979585/photo/goat-with-his-tongue-out.jpg?s=612x612&w=0&k=20&c=9pE4Mlx9f5245CWJGtaodpG3JGN-c1iYA4JDQRCBxg0=",
        "photographerCredit": "John Carnemolla"
      },

      {
        "loc":"https://media.npr.org/assets/img/2022/12/09/squirreljump-28aafd8cd34db8db8604eb503509496394234554.jpg?",
        "photographerCredit":"Alex Pansier"
      },
      
      {
        "loc":"https://images.unsplash.com/photo-1618265341355-d0e2d1fdf26b?q=80&w=1964&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        "photographerCredit":"James Watson"
      },

      {
        "loc":"https://media.istockphoto.com/id/1085112772/photo/funny-monkey-in-the-peruvian-jungle.jpg?s=612x612&w=0&k=20&c=kqhI7yj0_2d9h_Ignhn1EwaEkiIM48QS98LffEfMBbQ=",
        "photographerCredit":"Damian S"
      },
       
      {
        "loc":"https://media.istockphoto.com/id/1175942160/photo/harbor-seal.jpg?s=2048x2048&w=is&k=20&c=cz2rFVTKn8Pgur2-qQjEaMvq5a-zMc-wtumIKicYmRA=",
        "photographerCredit":"Mauribo"
      }
    ]);
    const index2 =ref(0);
    const imagechangeRight = function () {
      // Decrement index
      index2.value--;
      // Catch too low a number
      if (index2.value < 0){
        index2.value = images2.value.length - 1;
      }
    };

      const startSlideshow = () => {
        const interval = setInterval(imagechangeRight, 5000); // Change image every 5 seconds

      
      };

     
    
    onMounted(() => {
      startSlideshow();
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
      // add onclick (image location, imagechange and index
      // imgLoc,
      imageLeft,
      imagechangeRight,
      index,
      index2,
      images,
      images2
      
    }
  },
});

</script>

<!-- <script src="./node_modules/axios/dist/axios.min.js">

</script> -->
<template>
  <header style="background-color: rgb(47, 47, 170);">
   <p style="text-align: center;"><span style="color: white; font-size: 40px;">Workplace breather</span></p>
    <br>
  <br>
  
  </header>

<body>
  
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
      @click="imageLeft" 
      height="300px" width="300px" 
      :src="images[index].loc">
      <br>
      Picture credit goes to:
      <p>{{images[index].photographerCredit }}</p>
     

    </div>
    <div class="row image">
      <br>
      <p> Or we can click for you here</p>
      <img
      @startSlideshow="imagechangeRight" 
      height="300px" width="300px"
      :src="images2[index2].loc" >
      <br>
      Picture credit goes to:
      <p>{{images2[index2].photographerCredit }}</p>
    </div>
  </div>
  
</body>
    
  
</template>

<style>

.header {
  border-style: dotted;
  border-color: brown;
background-color: rgb(47, 47, 170);
text-align: center;
}

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
margin: 100px;
}

.smallimg {
  height:300px;

} 
.span {
  color: white; font-size: 40px; text-align: center;
}

</style>

