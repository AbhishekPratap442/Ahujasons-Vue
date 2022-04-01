    <template>
    <div>
        <div class="products_img">
            <div class="side_filter">
                <div>
                    <p>{{topWearKurtas}}</p>
                    <h3 class="filter_type" v-for="filter in productFilter " :key="filter.id">
                     {{filter.filter_lable}}
                        <span> <svg xmlns="http://www.w3.org/2000/svg"
                                height="24px"
                                viewBox="0 0 24 24"
                                width="24px"
                                fill="#000000"><path d="M0 0h24v24H0V0z" fill="none" /><path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z" /> </svg>
                        </span>
                    <!-- <p v-for="filter in productFilter " :key="filter.id">{{filter.options.total}}</p> -->
                     <ul class="filter_type_list" >
                        <li>
                            <input type="checkbox" for="vehicle1" />
                            <label>{{filter.options.value}}</label>
                        </li> </ul>
                    </h3>
                       
                </div>
            </div>

            <div class="products_div">
                <div class="products">
                    <div class="api_products">
                        <div v-for="item in list" :key="item.id">
                            <div id="productImg">
                                <img :src="item.image" />
                            </div>
                            <h4>{{ item.name }}</h4>
                             <span>Rs{{ item.selling_price }}</span>  <span id="discount">  -{{item.discount}}% </span>
                            <p>Size {{ item.size }}</p>
                            <span id="stock">{{ item.stock_status }}  </span> 
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

    <script>
// import axios from "axios"

export default {
    name: 'Products',
props:{
      list:Array,
       productFilter:Array,
       topWearKurtas:String
    },
    // data() {
    //     return {
    //         list: []
    //     }


    // },


    // methods: {

    //     async apiCall() {
    //         let data = await axios.get('https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter=')
    //             console.log("list", this.list),
    //                 this.list = data.data.result.products;

    //         // console.log("eee", this.list);
    //         // for(let i=0; i < this.list.length; i++){
    //         //     console.log(this.list[i].image)
    //     }
    //     //           .then( data => {
    //     //   console.log(data)
    //     //   this.list = data.data.result.products
    //     //   console.log("list ", this.list)
    //     //   }, 
    //     //   );

    // },
    // mounted() {

    //     this.apiCall()
    //       console.log("API DATA")
    // }
}

</script>
    <style scoped>

    .productImg{
        width: 75%;
    }
    .productImg img{
        width: 100%;
    }
.products_img {
    max-width: 1600px;
    margin: auto;
    display: flex;
    padding: 23px;
}
.products_div {
        width: 100%;
}
.api_products {
    /* position: relative; */
    display: flex;
    justify-content: space-evenly;
    flex-wrap: wrap;
    /* width: 95%; */
    align-items: center;
    /* /* padding: 7px; */
}
#discount{
    color: red;
    padding: 0px 15px;
}
#stock{
    color: green;
}
.products_img img {
    /* width: 100%; */
}
.products {
    flex: 0 0 21%;
    position: relative;
}
.products svg {
    top: 9px;
    position: absolute;
    right: 0;
}
.products p {
    position: relative;
    color: #4c0b36;
}
.filter_type{
    display: flex;
    font-size: 14px;
    font-weight: 100;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid;
}
.side_filter {
    padding: 23px;
    /* display: none; */
}
.filter_type span svg{
    width: 15px;
}
.filter_type_list {
    list-style: none;
    padding: 23px;
}








@media (max-width: 767px){
    
    
.products svg {
    right: 0px;
  }
  .products h4 {
    font-size: 14px;
  }

  .products {
    position: relative;
    display: inline-block;
    margin: auto;
    }
  .products_img {
    padding: 0;
    display: flex;
    flex-wrap: wrap;

    border-bottom: 0px;
  }
  .products_img img {
      margin: 2px;
    max-width: 100%;
  }
  .products {
      flex: 0 0 45%;
  }
  .products p {
      margin: 7px 3px;
  }
  .products svg {
    position: absolute;
  
  }
  .api_products {
    /* position: relative; */
    display: flex;
    justify-content: space-evenly;
    flex-wrap: wrap;
    /* width: 95%; */
    align-items: center;
    /* /* padding: 7px; */
}
      }
</style>