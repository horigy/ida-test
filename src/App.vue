<template>
  <div id="app">
    <div class="container">
      <Form/>
      <List/>
    </div>
  </div>
</template>

<script>
import Form from '@/components/Form.vue'
import List from '@/components/List.vue'
export default {
  name: 'App',
  components: {
    Form,
    List
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@400;600&display=swap');
@import url('https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.min.css');

* {
  box-sizing: border-box;
}

#app {
  font-family: 'Source Sans Pro', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background:#FFFEFB;
  text-align: center;
  color: #3F3F3F;
  line-height: 1.3;
  font-weight: 400;
}

.container {
  display: flex;
  flex-direction: row;
  padding: 32px;
  width: 100%;
  max-width: 1440px;
  margin: 0 auto;
}

</style>
