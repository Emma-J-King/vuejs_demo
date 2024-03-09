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
</script>

<!-- <script src="./node_modules/axios/dist/axios.min.js">

</script> -->
<template>
  <header>
    <div class="wrapper">
      <HelloWorld msg="Do you like jokes?" />
    </div>
   
  </header>

  <main>
    {{ joke }}
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>

