<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <Node></Node>
<!--    <Vode></Vode>-->
  </div>
</template>

<script>

// import Vode from "./Vode";
import Node from "./Node";
export default {
  name: 'HelloWorld',
  components: {Node},
  props: {
    msg: String
  },
  data() {
    return {}
  },
  created() {

  },
  methods:{}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
