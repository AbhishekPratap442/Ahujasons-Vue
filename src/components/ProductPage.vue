<template>
  <div>
    <div class="filters">
      <div
        class="left_filter"
        v-on:click="filterSeen = !filterSeen"
        @click="getfilteroptions"
      >
        <h3 v-on:click="showfilter = !showfilter">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="18.467"
            height="11.654"
            viewBox="0 0 18.467 11.654"
          >
            <g transform="translate(-1149.5 42.429)">
              <rect
                width="8.992"
                height="1.869"
                transform="translate(1149.5 -40.656)"
              />
              <rect
                width="3.932"
                height="1.869"
                transform="translate(1164.035 -40.656)"
              />
              <rect
                width="8.992"
                height="1.869"
                transform="translate(1167.967 -32.406) rotate(-180)"
              />
              <rect
                width="3.932"
                height="1.869"
                transform="translate(1153.432 -32.406) rotate(-180)"
              />
              <rect
                width="1.74"
                height="5.35"
                transform="translate(1160.393 -42.429)"
              />
              <rect
                width="1.74"
                height="5.35"
                transform="translate(1154.987 -36.124)"
              />
            </g>
          </svg>
          <span @click="toggleDetails">{{
            detailsAreVisible ? "HIDE FILTER" : "SHOW FILTER"
          }}</span>
        </h3>
      </div>

      <div class="right_filter">
        <select
          name="shrot_by"
          id="shrot_by"
          @change="sortingdatabyprice()"
          v-model="shrot_by"
        >
          <option selected>SORT BY</option>
          <option
            :value="sort.code"
            v-for="sort in productsSort"
            :key="sort.id"
          >
            {{ sort.label }}
          </option>
        </select>
      </div>
    </div>

    <div class="products_img">
      <div class="side_filter" v-if="filterSeen">
        <div>
          <h3
            class="filter_type"
            v-for="filters in productFilter"
            :key="filters.id"
          >
            <div
              v-on:click="filters.isVisible = !filters.isVisible"
              class="filter_type_option"
            >
              <span>{{ filters.filter_lable }}</span>
              <span>
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  height="24px"
                  viewBox="0 0 24 24"
                  width="24px"
                  fill="#000000"
                >
                  <path d="M0 0h24v24H0V0z" fill="none" />
                  <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z" />
                </svg>
              </span>
            </div>
            <div class="btn">
              <!-- <button @click="applyfilter">Apply Filter</button> -->
            </div>
            <div>
              <div class="filter_type_sub_option" v-if="filters.isVisible">
                <ul v-for="option in filters.options" :key="option.value_key">
                  <label class="checkbox" for="check1">
                    <input
                      type="checkbox"
                      name="check1"
                      @click="
                        sortingdatabyfilter($event, option.value, option.code)
                      "
                      :id="option.value_key"
                    />
                    <span class="checkmark"></span>
                    <span class="label">
                      {{ option.value }} ({{ option.total }})</span
                    >
                  </label>
                </ul>
              </div>
            </div>
          </h3>
        </div>
      </div>

      <div class="api_products">
        <div v-for="item in list" :key="item.id" class="api_products_img">
          <div class="productImg">
            <img :src="item.image" />
            <div class="productsSpecs">
              <h4>{{ item.name }}</h4>
              <span>Rs{{ item.selling_price }}</span>
              <span id="discount">-{{ item.discount }}%</span>
              <span id="stock">{{ item.stock_status }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "ProductsPage",
  data: {
    seen: true,
  },
  data() {
    return {
      list: [],
      productFilter: [],
      productFilterCetegory: [],
      productsSort: [],
      seen: true,
      toggle: true,
      detailsAreVisible: false,
      filterSeen: false,
      showfilter: false,
      isVisible: false,
      shrot_by: "",
      value: "",
      filtersoptions: "",
      checkparam: "",
    };
  },
  methods: {
    async wforwomendata() {
      let data = await axios.get(
        `  https://pim.wforwoman.com/pim/pimresponse.php`,
        {
          params: {
            service: "category",
            store: 1,
            url_key: "top-wear-sets-dresses",
            page: 1,
            count: 20,
            sort_by: this.shrot_by,
            sort_dir: "desc",
            filter: this.filtersoptions,
          },
        }
      );
      this.productFilter = data.data.result.filters;
      console.log("this is product list", this.list);
      this.list = data.data.result.products;
      this.productsSort = data.data.result.sort;
    },

    sortingdatabyfilter(event, value, code) {
      console.log("event=", event, "value=", value, "code=", code);
      // this.filtersoptions.push(code + "-" + value);
      this.filtersoptions = `${code}-${value}`;
      this.wforwomendata();

      if (event.target.checked) {
        const coma = "";
        if (this.filtersoptions !== "") {
          coma = " ,";
        }
        this.filtersoptions = `${this.filtersoptions}${coma}${code}-${value}`;
        this.wforwomendata();
      } else {
        this.filtersoptions = this.filtersoptions.replaceAll(
          code + "-" + value,
          ""
        );

        const id = event.target.id;
        for (let data of this.filtersoptions) {
          if (data === id) {
            const index = this.filtersoptions.indexOf(data);
            //  console.log(index)
            this.filtersoptions.splice(index, 1);
          }
        }
      }
      console.log(this.productFilterCetegory);
      this.wforwomendata(this.productFilterCetegory);
      console.log(this.productFilterCetegory);
    },
    applyfilter() {
      const pars = this.productFilterCetegory.map((str) => {
        return str;
      });
      const data = {
        productFilterCetegory: pars,
      };
      console.log(data);
    },

    getfilteroptions() {
      this.wforwomendata();
    },

    sortingdatabyprice(shrot_by) {
      // this.$emit("sorting-data-by-price", this.shrot_by);
      console.log("this is sort filter", this.shrot_by);

      this.checkparam = shrot_by;
      console.log("this is a event 1", this.shrot_by);
      this.wforwomendata();
      //  this.lowtohigh=desc
      // this.productsSort
    },

    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
  },

  mounted() {
    this.wforwomendata();
  },

  props: {
    // list: Array,
    // productFilter: Array,
    // productsSort: Array,
  },
};
</script>
<style scoped>
.hide {
  display: none;
}
body {
  box-sizing: border-box;
  margin: 0 auto;
  padding: 20px;
}
.filters {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 26px;
}
.left_filter {
  border: 1px solid;
  padding: 12px 12px;
  cursor: pointer;
}
.left_filter h3 {
  font-size: 12px;
  font-weight: 100;
}
.left_filter h3 svg {
  width: 14px;
  padding: 0px 9px;
}

.right_filter {
  border: 1px solid;
}
.right_filter select {
  border: none;
  padding: 12px 15px;
  cursor: pointer;
  width: 226px;
  height: 41px;
  font-weight: 100;
  font-size: 13px;
  font-family: "Jost";
}

.right_filter select option {
  padding: 12px 12px;
}
/* Customize the label (the container) */
.check-box-group {
  display: flex;
  flex-direction: column;
}

.checkbox {
  cursor: pointer;
  display: flex;
  align-items: center;
  margin: 10px 0;
}

.checkbox .label {
  font-size: 12px;
  margin: 0 10px;
}

.checkbox .checkmark {
  width: 12px;
  height: 12px;
  border: 1px solid;
  display: inline-block;
  border-radius: 0px;
  background: #4c0b36
    url(https://upload.wikimedia.org/wikipedia/commons/thumb/2/27/White_check.svg/1200px-White_check.svg.png)
    center/1250% no-repeat;
}

.checkbox input:checked + .checkmark {
  background-size: 60%;
}

.checkbox input {
  /* display: none; */
}

/* -------------------------------------Products -------------------- */
.products_img {
  display: flex;
  padding: 26px;
  box-shadow: 0px 5px 0px -4px #e4e4e4;
}
.side_filter {
  padding-right: 22px;
  width: 18%;
}
.filter_type {
  font-size: 14px;
  font-weight: 100;
}
.filter_type_option {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid;
  margin-bottom: 18px;
}
.filter_type_option span {
  margin: 9px 0px;
}
.filter_type_sub_option ul {
  max-height: 250px;
  overflow: auto;
  display: flex;
  align-items: center;
  /* padding: 0px 4px; */
  list-style: none;
}
.filter_type_sub_option ul li {
  padding-left: 12px;
  /* width: 300px; height: 200px; overflow: auto */
}
svg {
  width: 15px;
}
#checkbox {
  color: red;
}
.api_products {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.api_products_img {
  width: 22%;
}
.productImg img {
  width: 100%;
}
.productsSpecs {
  margin-bottom: 29px;
}
.productImg h4 {
  font-size: 14px;
  font-weight: 100;
}
.productImg span {
  font-size: 14px;
  color: #4c0b36;
}
#discount {
  padding: 0px 22px;
  color: red;
}
#stock {
  font-size: 14px;
  color: green;
}

@media (max-width: 767px) {
  .api_products_img {
    width: 49%;
  }
  .filters {
    display: flex;
    padding: 0px;
    width: 100%;
    z-index: 222;
    position: fixed;
    bottom: 0;
    background-color: white;
    justify-content: space-evenly;
  }
  .left_filter {
    width: 48%;
  }
  .right_filter {
    width: 52%;
  }

  .right_filter select {
    padding: 13px 7px;
  }
  .side_filter {
    width: 100%;
    position: relative;
    background: #ffffff;
    border: none;
    top: -27vh;
    z-index: 1;
    left: 0px;
    padding: 26px;
  }

  .products_img {
    padding: 4px;
  }
  #shrot_by {
    width: 93%;
  }
}
</style>
