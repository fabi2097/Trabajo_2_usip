<template>
    <div class="container ">

<div class="row">
    <h4>Productos relacionados</h4>
</div>
<div class="row">
    <div class="col">
        <div class="card" style="width: 18rem;">
            <div class="card-body">
                <template v-for="(productoval, index) in productos" :key="index">
                    <div v-if="index==1">
                   <h5 class="card-title" v-if="productoval.nombre==='KF102'">{{productoval.nombre}}</h5>                                    
                   <img v-bind:src="productoval.imagen" alt="" width="200" v-on:click="caracteristicaproductorel(productoval.id)">
                   <p v-show="productosid.id==2 && valfalse" class="card-text">{{productosid.descripcion}}</p>
                   <div v-if="productoval.precio==='1180'" class="producto-relacionado-precio">Precio:{{productoval.precio}}</div>
                   <template v-for="valor in productoval.colores">
                   <div v-if="index==1" class="color-box" :style="'background:'+valor"></div>
                  </template>
                </div>
                </template>            
                <div>
             <div>
        </div>
                </div>
            </div>
        </div>
    </div>
    <div class="col">
        <div class="card" style="width: 18rem;">
            <div class="card-body">
                <template v-for="(productoval, index) in productos" :key="index">
                <div v-if="index==2" v-on:click="caracteristicaproductorel(productoval.id)">
                <h5 class="card-title">{{productoval.nombre}}</h5>
                <img v-bind:src="productoval.imagen" alt="" width="200">
                <p v-show="productosid.id==3 && valfalse" class="card-text"> {{productosid.descripcion}}
                </p>
                <div v-if="productoval.precio==='154'" class="producto-relacionado-precio">Precio:{{productoval.precio}} BOB</div>
                </div>
                <template v-for="(valor,index1,el) in productoval.colores">
                    <div v-if="index==2" class="color-box" :style="'background:'+valor"></div>
                   </template> 
                </template>
                <div>
        <div>
        </div>
                </div>
            </div>
        </div>
    </div>
    <div class="col">
        <div class="card" style="width: 18rem;">
            <div class="card-body">
                <template v-for="(productoval, index) in productos" :key="index">
                 <div v-if="index==3" v-on:click="caracteristicaproductorel(productoval.id)">
                    <h5 class="card-title">{{productoval.nombre}}</h5> 
                    <img  :src="productoval.imagen" alt="" width="200">    
                    <p v-show="productosid.id==4 && valfalse"  class="card-text">
                        {{productosid.descripcion}}</p>
                        <div v-if="productoval.precio==='1800'" class="producto-relacionado-precio">Precio:{{productoval.precio}} BOB</div>
                </div>     
                <template v-for="(valor) in productoval.colores">
                    <div v-if="index===3" class="color-box" :style="'background:'+valor"></div>
                   </template>   
                </template>
                <div>
        <div>
        </div>
                </div>
            </div>
        </div>
    </div>
</div>
</div>
  </template>
  
  <script>
  const api=process.env.VUE_APP_API;
  export default {
    name: 'ProductosRelacionados',
    data(){
    return{
        api,
        precioEstilos: "background: orangered; color: white; font-weight: bold",
        productos:[],
        productosid:[],
        idpopup:null,
        valfalse:false,
     }
   },
    methods:{
        getProductos(){
        this.axios({
                method: 'get',
                url:  this.api+'/Productos'
            })
                .then((response) => {
                    this.productos = response.data;
                    console.log(response);
                })
                .catch((error) => { console.log(error) })
                .finally(() => { });
       },
       caracteristicaproductorel(id){
        this.axios({
                method: 'get',
                url:  this.api+'/Productos/'+id
            })
                .then((response) => {
                    this.productosid = response.data;
                    console.log(response);
                    this.valfalse=!this.valfalse;
                })
                .catch((error) => { console.log(error) })
                .finally(() => { });
       }
    },
    mounted(){
        this.getProductos();
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped lang="scss">
  .color-box {
                width: 40px;
                height: 40px;
                border-radius: 50%;
                margin: 7px;
                display: inline-block;
            }

            .clic{
                cursor: pointer;
            }

            .quantity button{
                border-radius: 50%;
                display: inline-block;
                width: 30px;
            }
            .quantity div{
                text-align: center;
                min-width: 30px;
                display: inline-block;
                font-weight: bold;
            }
            .buy-box{
                margin: 20px;
            }
            footer {
                
                text-align: center;
                padding: 30px 10px;
                margin-top: 50px;
                min-height: 100px;
            }
            .container{
                margin-top: 50px;
            }
            .producto-relacionado-precio{
                background: orangered;
                color: white;
                text-align: center;
                padding: 10px; 
            }
  </style>
  