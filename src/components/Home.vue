<template>
  <div class="header">
    Virtual Random Keyboard
  </div>
</template>

<script>
export default {
  name: 'Home',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header{
  display: flex;
  align-content: flex-end;
  justify-content: flex-end;
  margin-top: 25px;
  right: 5px;
  font-size: 22px;
  background: white;
  /* background: black; */
  position: absolute;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

</style>
