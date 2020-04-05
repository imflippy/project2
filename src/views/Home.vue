<template>
  <div class="home">
      <div class='table'>
          <div class='row'>
              <select v-model="formData.idProd" class='width25'>
                <option value="0">Choose Prodcut</option>
                <option v-for="prod in showFreeProducts" :value="prod.id" :key="prod.id">{{ prod.name }}</option>
              </select>
              <input class='width25' type="number" v-model="formData.quantity" placeholder="Quantity" >
              <span v-if="this.formData.idProd == 0 || this.formData.quantity <= 0 " class='price width25'>$0</span>
              <span v-else class='price width25'>${{ calculatePrice(formData.idProd, formData.quantity)}}</span>
              <!-- <font-awesome-icon icon="trash"/> -->
              <button type="button" @click="addProd()" class='width25' v-if="this.formData.idProd == 0 || this.formData.quantity <= 0 " disabled>Insert</button>
              <button type="button" @click="addProd()" class='width25' v-else>Ubaci</button>
          
          </div>
          <div class='row' v-for="oneRow in selected" :key="oneRow.id">
              <span class='width25'>{{ filterObj(oneRow.id).name }}</span>
              <span class='width25'> {{ oneRow.quantity }}</span>
              <span class='price width25'>$ {{ oneRow.sum }}</span>            
              <span class='width25'><a href="#" class="kanta" @click="deleteProd(oneRow.id)"><font-awesome-icon icon="trash" /></a></span>
          </div>
          <div class='sumCalculated'>
            <p class="total">Total Price: ${{ calculateSum }}</p>
            <button v-if="selected.length == 0" class="sendRequest" disabled type="button">Send Request</button>
            <button v-else class="sendRequest" @click="sendRequest()" type="button">Send Request</button>

          </div>
        
      </div>
      <div class='json'>
        {{ json }}  
      </div>
      
  </div>
</template>

<script>
import products from '../data/product.json'

export default {
  name: "Home",
  data() {
    return {
      products,
      selected: [
      ],
      formData: {
        idProd: 0,
        quantity: 0
      },
      json: ''
    }
  },
  methods: {
    filterObj(id){
      let scoped = this.products.filter(item => {
        return parseInt(item.id) === parseInt(id);
      })
      return scoped[0];
    },
    calculatePrice(id, quantity) {
      let object = this.filterObj(id);
      if(quantity < 10) {
         return object.price1 * quantity;
      } else {
        return object.price2 * quantity;
      }
    },
    addProd() {
      this.selected.push({
          id: this.formData.idProd,
          quantity: this.formData.quantity,
          sum: this.calculatePrice(this.formData.idProd, this.formData.quantity)
      });

      this.formData.idProd = 0;
      this.formData.quantity = 0;
    },
    deleteProd(id) {
        let rest = this.selected.filter(item => {
        return parseInt(item.id) !== parseInt(id);
      })
      return this.selected = rest;
      
    },
    sendRequest() {
      this.json = '[';
      this.selected.forEach(p => {
        this.json += `
          {
            'id': ${p.id},
            'quantity': ${p.quantity},
            'sum': ${p.sum}
          },
        `;
        
      })
      this.json += ']'
      this.selected = [];
      
    }
  },
  computed: {
    showFreeProducts() {
      let productsToShow = [];
      this.products.forEach(p => {
          if(this.selectedId.indexOf(p.id) === -1) {  
            productsToShow.push(p);
          }        
      })
      return productsToShow;
    },
    selectedId() {
      let ids = [];
      this.selected.forEach(p => {
          ids.push(p.id); 
      });
      return ids;
    },
    calculateSum() {
      let sum = 0;
        this.selected.forEach(p => {
           sum += this.calculatePrice(p.id, p.quantity);
        })
        return sum;
    }
  }
};
</script>

<style lang='scss' scoped>
  .home {
    display: flex;
    align-items: center;
    height: 100%;
    position: relative;
  }
  .table {
      width: 80%;
      height: 80%;
      margin: 0 auto;
      overflow: auto;
      border: 1px solid #797b80;
      padding: 15px;
      font-size: 16px;
      position: relative;
      .row {
        display: flex;
        justify-content: space-between;
        height: 22px;
        margin: 5px;
        color: #797b80;
        .kanta {
          color: #797b80;

        }
        .width25 {
          width: 23%;
          text-align: center;
        }
      }
    .sumCalculated {
      display:flex;
      position: absolute;
      bottom: 0;
      .total {
        color:#41B883;
        font-size: 20px;
      }
      .sendRequest {
        background-color: #41B883;
        border: none;
        margin-left: 15px;
        margin-bottom: 3px;
      }
    }
  }
  .json {
      position: absolute;
      bottom: 0px;
    }
</style>
