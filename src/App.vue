<template>
<div id="app">
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container">
    <a class="navbar-brand" href="#">
     <img src="./assets/img/Logo.webp" alt="GradGen Logo" width="100px">
     </a>
  </div>
</nav>
<div id="bodybg">
<div class="container text-center">
    <h2 class="page-title">Linear Gradient Generator</h2>
    <br />
    <h3 class="page-subtitle">Pick the Color Range and Publish Swatch</h3>
    <br />
 <div class="mx-auto" width="100px">
 <b-form-input width="100px" type="color" v-model="value1" ref="value1" id="colorone"></b-form-input>
 <b-form-input width="100px" type="color" v-model="value2" ref="value2" id="colortwo"></b-form-input>
</div>
<br />
    <div class="btn-group">
    <button type="button" id="pubBtn" @click="addSwatch" class="navbar ml-auto btn btn-lg btn-success" >Publish</button>
    <button type="button" id="editBtn" @click="editSwatch" class="navbar ml-auto btn btn-lg btn-info" >Edit</button>
    <button type="button" id="saveBtn" class="navbar ml-auto btn btn-lg btn-warning" >Save</button>
    <button type="button" id="delBtn" @click="deleteSwatch" class="navbar mr-auto btn btn-lg btn-primary" >Delete</button>
    </div>
<b-form-input
    v-if="getName"
    placeholder="Name Swatch &amp; Publish or Save Edited Swatch"
    @keypress="newSwatch"
    v-model="value3"
    ref="value3"
    id="name"
    size="lg"
    type="text"
    class="search-bar"
/>
</div>
 </div>
 <b-jumbotron class="text-center">
   <template v-slot:header>Gradient Swatch Generator</template>
   <template v-slot:lead>
    Linear Gradient Swatch Generator, Select Two Color Values and Publish.<br />
    Select Individual Swatch to Edit or Delete.
 </template>
<div class="container-fluid bg-3 text-center">
<h3>Your Gradients</h3><br>
<div class="row gallery">
<div v-for="item in items" :key="item.id" class="col-md-3 swatch">
<div :style="{ backgroundImage: 'linear-gradient('+item.color1 +','+item.color2 +')'}" class="bg-gradient">
</div>
<div id="info">
<h5>{{ item.name }}</h5>
<p>{{ item.color1 }} {{ item.color2}}</p>
</div>
</div>
</div>
</div>
</b-jumbotron>
<Footer />
</div>
</template>
<script>
import Footer from '@/components/Footer'
//import Vue from "vue";
export default {
  components: {
    Footer
 },
  data: () => ({
    // color1: null,
    // color2: null,
    // name: null,
    items : [
      {
      id : 1,
      color1 : '#1be7d1',
      color2 : '#141dbe',
      name: 'Mystic Blue'
      },
      {
      id : 2,
      color1 : '#e91ab0',
      color2 : '#be147b',
      name: 'Fancypants Pink'
      }
    ]
  }),
  computed : {
    gradientStrings () {
      return this.items.map(this.colorString)
    }
  },
  methods : {
    newSwatch () {
      this.$emit('input', {
      color1: +this.value1,
      color2: +this.value2,
      name: +this.value3
      });
      return {
         id : this.items.length + 1,
         color1 : this.value1,
         color2 : this.value2,
         name: this.value3
      }
    },
    colorString (swatch) {
       return swatch.color1 + swatch.color2
    },
    //nameString(swatch) {
      //return swatch.name
   // },
    isUnique (swatch) {
       return !this.gradientStrings.includes(this.colorString(swatch))
    },
    addSwatch () {
       const swatch = this.newSwatch()
       if (this.isUnique(swatch)) {
       this.items.push(swatch);
       }
       console.log(swatch.color1);
       console.log(swatch.color2);
       //console.log(swatch.name);
    }
  }
}
</script>
<style>
@import url('https://fonts.googleapis.com/css?family=Shrikhand&display=swap');
@font-face {
  font-family: 'Shrikhand';
  src: url('https://fonts.googleapis.com/css?family=Shrikhand&display=swap');
  font-weight: normal;
  font-style: normal;
}
@media only screen and (min-device-width : 320px) and (max-device-width : 480px) {
#bodybg {
      height: 460px;
      min-height:460px;
   }
}
* {
 margin: 0;
 padding: 0;
 box-sizing:border-box;
}
/* Add a gray background color and some padding to the footer */
footer {
      display:flex;
      justify-content: center;
      align-items: center;
      background-color: gainsboro!important;
      padding:12px;
    }
    #editBtn,
    #saveBtn {
      display:none;
    }
    input#name {
      margin-top: 30px;
      border-radius: 8px 8px 8px 8px;
    }
    h4 {
    font-family:'Roboto';
    margin-top: 15px;
    text-transform: uppercase;
    color: #345678;
    }
    h3.page-subtitle {
    font-family:'Roboto';
    font-size: 24px;
    }
    h2.page-title {
      font-family: 'Shrikhand', cursive;
      font-size: 44px;
    }
    h1.display-3 {
      margin-top:20px;
      font-family: 'Shrikhand', cursive;
      font-size:52px;
    }
    .bg-gradient {
    display:inline-block;
    margin:10px;
    height: 180px;;
    width:100%;
    }
    #info {
    padding-top:8px;
    background-color:#fff;
    height: 55px;
    width:100%;
    }
    #info p {
      font-family:'Roboto';
      text-align:left;
      padding-left:0px;
      font-size: 0.8em;
      font-weight: 700;
    }
    #info h5 {
      font-family:'Roboto';
      text-align:left;
      text-transform: capitalize;
      padding-left: 0px;
      font-size: 0.9em;
      font-weight: 700;
    }
.bg-gradient:focus,
.bg-gradient:hover,
.bg-gradient.active {
 border: solid 3px rgba(84, 112, 155, 0.7);
}
#bodybg {
padding-top: 40px;
height: 460px;
background-image: linear-gradient( to right,#0fb1d1,#0fb1d1);
}
input#colorone,
input#colortwo {
margin:5px;
cursor: pointer;
}
</style>
