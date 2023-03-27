<template>
  <div class="container">
    <div class="watches">
      <StopWatch v-for="(index) in watches" :key="index" />
      
      <div @click="addWatch" class="watch add_watch">
        +
      </div>
    </div>
  </div>
</template>

<script>
import StopWatch from './components/StopWatch.vue';

export default {
  data() {
    return {
      watches: 0, // Количество секундомеров на данный момент
    }
  },
  name: 'App',
  components: {
    StopWatch
  },
  methods: {

    // Добавление секудомера
    addWatch() {
      this.watches += 1
    }
  }
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Gotham Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 22px;
  color: #9E9E9E;
  min-height: 100vh;
  height: 100%;
  background: #353638;
}
.container{
  max-width: 1200px;
  margin: 0 auto;
  padding: 72px 20px;
}

.watches {
  display: flex;
  flex-wrap: wrap;
  gap: 50px;

  .watch {
    width: 225px;
    height: 120px;
  }

  .add_watch {
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #696969;
    font-size: 40px;
    cursor: pointer;
    transition: all .3s ease;

    &:hover {
      opacity: .7;
    }
  }
}



@media screen and (min-width: 1024px) {
  .container{
    max-width: 1200px;
    padding: 72px 212px;
  }
  
  .watch {
    flex-basis: calc(33.33% - 50px);
  }
}

@media screen and (max-width: 1024px) {
  .container{
    max-width: 768px;
    padding: 72px 135px;
  }
  
  .watch {
    flex-basis: calc(50% - 50px);
  }
}

@media screen and (max-width: 768px) {
  .container{
    max-width: 320px;
    padding: 72px 46px;
  }
  
  .watch {
    flex-basis: 100%;
  }
}

@font-face {
  font-family: "Gotham Pro";
  src: url("./fonts/gothampro.ttf");
}
</style>
