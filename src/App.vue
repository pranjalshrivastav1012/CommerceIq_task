/* eslint-disable no-unused-vars */



<template>
<div class="nav-bar"></div>
<div class="main">
   <Home/>
   <textarea
      ref='focusMe'
      type="text"
      v-model="input"
      class="jumbotron"/>
  
   <div class="keyboard">
    <div class="keys" v-for="(i) in items" :key="i.id" >
      <div v-for="(j) in i" :key="j.id">
        <Button class="key_button" @click="pressedLetter(j)" >{{formatLetters(this.flag, j)}}</Button>
      </div>
    </div>
    <div class="function_keys">
      <Button 
     val="tab"
     className="tab"
      variant="contained"
      @click="onTabPress()"
     >tab</Button> 
    <Button 
     className="capslock"
     id="capslock"
      val="Caps Lock"
      @click="onCapsPress()"
      >caps lock
      </Button>
      
      <Button
      className="shift"
      id="shift"
      @click="onShiftPress(!this.shiftFlag)"
      val="shift"
      variant="contained"
      >shift
      </Button>
      <Button 
      val="space"
      className="space"
      variant="contained"
     @click="onSpacePress()"
      >space
      </Button>
      <Button 
     val="backspace"
     className="backspace"
      variant="contained"
      @click="onBackspacePress()"
     >backspace</Button>
       <Button 
     val="enter"
     className="enter"
      variant="contained"
      @click="onEnterPress()"

      >enter</Button>
    </div>
    </div> 
</div> 
</template>

<script>

import Home from './components/Home.vue'

export default {
  name: 'App',
  data(){
    return{
      input: '',
      flag: false,
      shiftFlag: false,
      items: [['1','2','3','4','5','6','7','8','9','0'],
    ['Q','W','E','R','T','Y','U','I','O','P'],
    ['A','S','D','F','G','H','J','K','L',';'],
    ['Z','X','C','V','B','N','M',',','.','/']],
    }
  },
  components: {
    Home,
    
  
    // Button 
  },
  
  mounted () {

    setTimeout(() => {
       this.$refs.focusMe.focus();
    }, 1);

  },
  methods:{
    shuffleLetters(){
      let value_temp = this.items;
      for (var i = 0; i < value_temp.length; i++) {
        for (var j = 0; j < value_temp[i].length; j++) {
            var i1 = Math.floor(Math.random() * (value_temp.length));
            var j1 = Math.floor(Math.random() * (value_temp.length));
            var temp = value_temp[i][j];
            value_temp[i][j] = value_temp[i1][j1];
            value_temp[i1][j1] = temp;
        }
      }
      this.items = value_temp;
    },getMapKey(map, searchValue) {
      for (let [key, value] of map.entries()) {
        if (value === searchValue)
          return key;
      }
    },
    pressedLetter(letter){
        var vm = this
        if(this.flag == false){
          vm.input += letter.toLowerCase()
        } else {
          vm.input += letter.toUpperCase()
        }
        this.shuffleLetters()
        if(this.shiftFlag){
          this.shiftFlag = false
          this.onShiftPress(this.shiftFlag)
        }
         this.mounted()
    },
    onTabPress(){
      var vm = this
      vm.input += "    "
    },
    onSpacePress(){
      var vm = this
      vm.input += " "
    },
    onBackspacePress(){
      this.input = this.input.substring(0, this.input.length - 1 )
    },
    onEnterPress(){
      var val = this
      val.input += "\n"
    },
    onCapsPress(){
      this.flag = !this.flag
      if(this.flag){
        document.getElementById("capslock").style.background = "#33675C";
      } else {
        document.getElementById("capslock").style.background = "rgba(38, 160, 48, 0.2)";
      }
    },onShiftPress(flag){
      var map = new Map();
      map.set('1','!');
      map.set('2','@');
      map.set('3','#');
      map.set('4','$');
      map.set('5','%');
      map.set('6','^');
      map.set('7','&');
      map.set('8','*');
      map.set('9','(');
      map.set('0',')');
      for(var i = 0; i<4; i++){
        for(var j = 0; j<10; j++){
          if(map.get(this.items[i][j]) && flag){
            this.items[i][j] = map.get(this.items[i][j])
          }
          if(this.getMapKey(map, (this.items[i][j])) && !flag){
            this.items[i][j] = this.getMapKey(map, (this.items[i][j]))
          }
        }
      }
      this.shiftFlag = flag
      if(flag){
        document.getElementById("shift").style.background = "#33675C";
        this.onCapsPress()
         document.getElementById("capslock").style.background = "rgba(38, 160, 48, 0.2)";
      } else {
        document.getElementById("shift").style.background = "rgba(38, 160, 48, 0.2)";
        this.onCapsPress()
      }
      
    },formatLetters(flag, j){
      if(flag){
        return j.toUpperCase()
      } else {
        return j.toLowerCase()
      }
    },
    
  }
}
</script>


<style>
#app {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  position: relative;
  
}
.jumbotron{
 
  margin-top: 120px;
  height: 90px;
  width: 90%;
  font-size: 20px;
}

.nav-bar {  
  position: absolute;
  background: linear-gradient(-90deg, #26a030, #33675C);
  height: 60px;
  margin-bottom: 25px;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.57);
  width : 110% ;
  margin-left: -10px;
  margin-top: -10px;
}

.keys{
 display: flex;
    flex-direction: row;
    bottom: 40px;
    margin-left:70px;
}
.key_button{
 
 height: 65px;
    width: 65px;
    font-size: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: white;
    margin: 3px;
    border-radius: 4px;
    border: none;
    background: rgba(38, 160, 48, 0.2);
    position: relative;
    
    bottom: 40px;   
    
}
.key_button:hover {
   background-color: #33675C;
    cursor: pointer;

}   

.keyboard{
  display: flex;
  justify-content: center;
  align-content: center;
  flex-direction: column;
  position: fixed;
  bottom: 0;
  right: 0;
  margin-right: 350px;
  
  
} 
.function_keys{
  display: flex;
  flex-direction: row;
}
.capslock{
   height: 65px;
  width: 90px;
    display: flex;
   justify-content: center;
      align-items: center;
    
    background-color: white;
    margin: 3px;
   
    border-radius: 4px;
    border: none;
    background: rgba(38, 160, 48, 0.2);
    position: relative;
    bottom: 40px;   
}
.capslock:hover{
  background-color: #33675C;
  cursor: pointer;
}

.shift{
   height: 65px;
  width: 80px;
    display: flex;
     justify-content: center;
      align-items: center;
    background-color: white;
    margin: 3px;
    border-radius: 4px;
    border: none;
    background: rgba(38, 160, 48, 0.2);
    position: relative;
    
    bottom: 40px;   
}
.shift:hover{
  background-color: #33675C;
  cursor: pointer;
}
  .space{
    height: 65px;
  width: 300px;
  display: flex;
    justify-content: center;
    align-items: center;
    background-color: white;
    margin: 3px;
    border-radius: 4px;
    border: none;
    background: rgba(38, 160, 48, 0.2);
    position: relative;
    
    bottom: 40px;   
  }
  .shift:hover{
  background-color: #33675C;
  cursor: pointer;
}
  .backspace{
    height: 65px;
  width: 75px;
  display: flex;
     justify-content: center;
      align-items: center;
    background-color: white;
    margin: 3px;
    border-radius: 4px;
    border: none;
    background: rgba(38, 160, 48, 0.2);
    position: relative;
    
    bottom: 40px;   
  }

  .backspace:hover{
  background-color: #33675C;
  cursor: pointer;
}

  .enter{
height: 65px;
  width: 80px;
  display: flex;
     justify-content: center;
      align-items: center;
    background-color: white;
    margin: 3px;
    border-radius: 4px;
    border: none;
    background: rgba(38, 160, 48, 0.2);
    position: relative;
    
    bottom: 40px;   
  }
.enter:hover{
  background-color: #33675C;
  cursor: pointer;
}
.tab{
height: 65px;
  width: 50px;
  display: flex;
     justify-content: center;
      align-items: center;
    background-color: white;
    margin: 3px;
    margin-left: 74px;
    border-radius: 4px;
    border: none;
    background: rgba(38, 160, 48, 0.2);
    position: relative;
    
    bottom: 40px;   
}
.tab:hover{
  background-color: #33675C;
  cursor: pointer;
}
</style>
