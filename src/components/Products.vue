    <template>
        <div>
            <div class="products_img">
                            <div class="side_filter">
                <div>
            <h3 class="filter_type">TYPES IN SHAWL  <span><svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 0 24 24" width="24px" fill="#000000">
                <path d="M0 0h24v24H0V0z" fill="none" />
                <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z" />
            </svg></span></h3>
            <ul class="filter_type_list" >
                <li><input type="checkbox" for="vehicle1"/><label> Plain</label></li>
                <li><input type="checkbox" for="vehicle1">/  <label > ari Border </label></li>
                <li><input type="checkbox" for="vehicle1"/> <label > Moonligh</label></li>
                <li><input type="checkbox" for="vehicle1"/> <label > Reversible</label></li>
                <li><input type="checkbox" for="vehicle1"/> <label > Ikat / check / stripes</label></li>
                <li><input type="checkbox" for="vehicle1"/> <label > Border embroidery / Palla</label></li>
                <li><input type="checkbox" for="vehicle1"/>  <label > All over embroidery / Jaal</label></li>
                <li><input type="checkbox" for="vehicle1"/> <label > Kani </label></li>
                <li><input type="checkbox" for="vehicle1"/> <label > Kalamkari</label></li>
                <li><input type="checkbox" for="vehicle1"/> <label > Paper mache</label></li>
                <li><input type="checkbox" for="vehicle1"/> <label > Aabdar</label></li>
                <li><input type="checkbox" for="vehicle1"/> <label > Gulabdar</label></li>
                <li><input type="checkbox" for="vehicle1"/> <label > Jama</label> </li>
            </ul>
                    <h3>PRICE  <span><svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 0 24 24" width="24px" fill="#000000">
                    <path d="M0 0h24v24H0V0z" fill="none" />
                    <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z" />
                    </svg></span></h3>
                    <h3>DISCOUNT  <span><svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 0 24 24" width="24px" fill="#000000">
                    <path d="M0 0h24v24H0V0z" fill="none" />
                    <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z" />
                    </svg></span></h3>
                </div>

        </div>

                <div class="products_div">
                     <div class="products">
                         <div class="api_products">
                             <div v-for="item in list" :key="item.id" >
                                    
                                          <div>
                                              <img :src="item.image"     />
                                                
                                          </div>  
                                            <h4>{{item.name}}</h4>
                                            <p>Rs{{item.price}}</p>
                                    </div>
                            </div>
                    </div>
                </div>

        </div>
 </div>
        








    </template>

    <script>
    import axios from "axios"
    // import { list } from "postcss"
    export default{
        name:'Products',
        data() {
            return {
                list: []
            }
        },
        methods: {
            async apiCall(){
                let data = await axios.get('https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter=')
                // data.data.result.products.map(()=>{

                // })
                this.list = data.data.result.products;
                console.log("eee", this.list);
                for(let i=0; i < this.list.length; i++){
                    console.log(this.list[i].image)
                }
    //           .then( data => {
    //   console.log("list", this.list),
    //   console.log(data)
    //   this.list = data.data.result.products
    //   console.log("list ", this.list)
    //   }, 
    //   );
            }
        },
        mounted() {

         this.apiCall()
          console.log("API DATA")
    }
    }

    </script>
    <style scoped>

    .products_img {
        max-width: 1600px;
        margin: auto;
        display: flex;
        padding: 23px;
    }
    .products_div{
        /* width: 84%; */
    }
    .api_products{
            /* position: relative; */
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    /* width: 95%; */
    align-items: center;
    /* /* padding: 7px; */


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
    .side_filter{
        padding: 23px;
        display: none;
    }
    .filter_type_list{
        list-style: none;
        padding: 23px;
    }
    </style>