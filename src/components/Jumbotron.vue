<template>
  <div>
      <!-- <textarea name="area" id="area" cols="30" rows="10" value=""/> -->
       <textarea
      ref='focusMe'
      type="text"
      v-model="input"
      class="jumbotron"/>
  
  </div>
</template>

<script>
export default {
    name: 'Jumbotron',
    props:[],


}
</script>

<style>
.jumbotron{
 
  margin-top: 120px;
  height: 90px;
  width: 90%;
  font-size: 20px;
}
</style>