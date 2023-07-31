
  <template>
    <div>
      <template v-for="(valor,index) in productos">
        <div class="container" v-if="index==0">
          <div class="row"> 
            <h3>{{valor.nombre}}</h3> 
          </div>
          <div class="row">    
            <div class="col-12 col-sm-6 col-md-4 ">
              <img v-bind:src="valor.imagen" alt="" width="200">
            </div>
            <div class="col-12 col-sm-6  col-md-8">
              <h6 v-html="valor.descripción"></h6>        
              <div class="p-3 mb-2 text-white" :style="precioEstilos">
                Precio: {{valor.precio}} BOB
              </div>
              <h5>Colores</h5>
              <div>
                <div v-for="color in valor.colores" class="color-box clic" v-bind:style="'background:'+color" v-on:click="cambiovalor(valor.id,color)">
                </div>
              </div>
              <h5>Cantidad</h5>
              <div class="quantity">
                <button v-on:click="decrementarCantidad()">-</button> <div>{{ pedido.cantidad }}</div> <button v-on:click="incrementarCantidad()">+</button>
              </div>
              <div class="buy-box">
                <button v-on:click="mensajealert()" type="button" class="btn btn-primary" v-show="pedido.cantidad>=1">Comprar</button>
              </div>   
            </div>
          </div>
        </div>
      </template>
    </div>
</template>

<script>
export default {
  name: 'ProductoComponent',
  data(){
    const api=process.env.VUE_APP_API;
    return {
      api,
      precioEstilos: "background: orangered; color: white; font-weight: bold",
      productos:[],
      pedido: {
        id: null,      
        cantidad: 1,
        color: null                
      }
    }
  },
  created(){
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
    cambiovalor(id,colorv){
      this.pedido.id=id;
      this.pedido.color=colorv;
      console.log(this.pedido.id);
      console.log(this.pedido.color);
    },
    mensajealert(){
      if(this.pedido.color==null){
        alert("El color debe ser seleccionado para realizar una compra");
      }else{
        alert("el pedido tiene los siguientes valores:"+JSON.stringify(this.pedido))
      }
    },
    decrementarCantidad() {
      if (this.pedido.cantidad > 0) { 
        this.pedido.cantidad -= 1;
      }
    },
    incrementarCantidad() {
      this.pedido.cantidad += 1;
    },
  },
  mounted() {
    this.getProductos();
  },
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