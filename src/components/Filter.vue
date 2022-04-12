<template>
  <div>
    <div class="filters">
      <div class="left_filter" @click="toggleSide">
        <h3>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="18.467"
            height="11.654"
            viewBox="0 0 18.467 11.654"
          >
            <g transform="translate(-1149.5 42.429)">
              <rect width="8.992" height="1.869" transform="translate(1149.5 -40.656)" />
              <rect width="3.932" height="1.869" transform="translate(1164.035 -40.656)" />
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
              <rect width="1.74" height="5.35" transform="translate(1160.393 -42.429)" />
              <rect width="1.74" height="5.35" transform="translate(1154.987 -36.124)" />
            </g>
          </svg>SHOW FILTER
        </h3>
      </div>
      <div class="hide">
        <a href>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="18.467"
            height="11.654"
            viewBox="0 0 18.467 11.654"
          >
            <g transform="translate(-1149.5 42.429)">
              <rect width="8.992" height="1.869" transform="translate(1149.5 -40.656)" />
              <rect width="3.932" height="1.869" transform="translate(1164.035 -40.656)" />
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
              <rect width="1.74" height="5.35" transform="translate(1160.393 -42.429)" />
              <rect width="1.74" height="5.35" transform="translate(1154.987 -36.124)" />
            </g>
          </svg>HIDE FILTER
        </a>
      </div>

      <div class="right_filter">
        <select name="shrot_by" id="shrot_by" @click="sorting()" v-model="testVal">
          <option value="short">SORT BY</option>
          <option :value="sort.code" v-for="sort in productsSort" :key="sort.id">{{ sort.label }}</option>
        </select>
      </div>
    </div>
  </div>
</template>
<script>
// import { toggleSide } from "./status"
// const filters = [
// "Category",
// "Plus Size"

// ]
// import axios from "axios";

// export default {
//   name: "Filter",
//   props: {
//     productFilter: Array,
//     productsSort: Array,
//   },
//   data() {
//     return {
//       testVal: "",
//     };
//   },

//   methods: {
methods: {
    async apiCall(moreData){
      let resp = await axios.get(
      `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=${moreData.page}&count=${moreData.count}&sort_by=${moreData.sort_by}&sort_dir=${moreData.sort_dir}&filter=${moreData.filter}`
    );
    console.warn("api data", resp.data.result.filters);
    if(resp.data.response.success_message === "success"){
    this.products = resp.data.result.products;
    if(this.filters.length === 0){
      this.filters = resp.data.result.filters;
      this.sort = resp.data.result.sort;
      this.sort.forEach(element => {
        if(element.label === 'Price'){
          element.label = 'Price(Low to High)';
          element.sortBy = 'asc'
        } else {
          element.sortBy = 'desc';
        }
      });
      this.sort.push({ code: 'selling_price', label: 'Price(High to Low)', sortBy: 'desc'})
    }
    } else {
      this.products = [];
      this.error_message = resp.data.response.error_message;
    }
    },
    toggleButton(){
      this.detailVisible = !this.detailVisible
    },
    sorting() {
      this.moreData.sort_by = this.selectedSorting.code;
      this.moreData.sort_dir = this.selectedSorting.sortBy;
      this.apiCall(this.moreData)
    },
  
    filterProduct(checkbox, filter, heading) {
      console.log(heading)
      if(heading === 'Price'){
          filter.value = filter.value.replaceAll(' ', '+')
        }
      if (checkbox.target.checked) {
        var comaSeparate = ""
        if(this.moreData.filter !== ""){
           comaSeparate = ","
        }        
        this.moreData.filter = `${this.moreData.filter}${comaSeparate}${filter.code}-${filter.value}`
        this.apiCall(this.moreData);
      }else {
        this.moreData.filter = this.moreData.filter.replaceAll(filter.code+'-'+filter.value, '');
        const last = this.moreData.filter.charAt(this.moreData.filter.length - 1);
        const first = this.moreData.filter.charAt(0);
        if(last === ',' || first === ','){
          this.moreData.filter = last === ',' ?this.moreData.filter.slice(0, -1) : this.moreData.filter.slice(1, this.moreData.length)
        }
        this.apiCall(this.moreData);
      }
    },
  },













//     sorting() {
//       // if (this.lable == "price") {
//       //   this.productsSort = this.productsSort.sort(this.price);
//       // }else if(this.productsSort=="discount"){
//       //   this.productsSort=this.productsSort.sort(this.discount);
//       // }
//       axios
//         .get(
//           `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=discount&sort_dir=desc&filter=`
//         )
//         .then((response) => {
//           console.log("api is called", response);
//         });
//     },
    // filter() {
    //   console.log(this.filterSelected);

//     // }
//   },
// };
</script>
<style scoped>
.filters {
  display: flex;
  justify-content: space-between;
  
}
#shrot_by {
  font-family: "Jost* 500";
  padding: 12px 30px;
  border-radius: 0px;
}
.shrot_by_choice {
  display: none;
  position: absolute;
  z-index: 1;
  border: 1px solid;
  background-color: white;
}
.shrot_by_choice ul li {
  list-style: none;
  margin: 14px 4px;
}

.shrot_by_choice ul li a {
  margin: 16px 6px;
  text-decoration: none;
  color: #303030;
}
.hide {
  /* display: flex; */
  display: none;
  justify-content: center;
  align-items: center;
  border: 1px solid;
}
.hide a {
  font-size: 14px;
  font-weight: bold;
  text-decoration: none;
  color: black;
  padding: 0px 16px;
}
.hide a svg {
  margin: 0px 7px;
}
.left_filter {
  display: flex;
  /* display: none; */
  justify-content: center;
  align-items: center;
  border: 1px solid;
}
.left_filter h3 {
  font-size: 14px;
  font-weight: bold;
  text-decoration: none;
  color: black;
  padding: 0px 16px;
  cursor: pointer;
}
.left_filter a svg {
  margin: 0px 7px;
}
div button {
  background-color: rgb(246 246 246);
  border: none;
  padding: 7px 67px 8px 19px;
  border-radius: 2px;
  cursor: pointer;
}
.products_div {
  margin: auto;
  justify-content: space-between;
  display: flex;
  flex-wrap: wrap;
}
.side_filter {
  width: 100%;
  display: none;

  transform: translateX(-20vw);
  transition: all 0.5s ease-in-out;
}
.side_filter h3 {
  font-size: 16px;
  font-weight: 100;
  padding: 13px 0px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid;
  width: 76%;
}
.side_filter ul li {
  padding: 10px;
}
.filter_type_list {
  display: none;
}
.filter_type_list_display {
  display: block;
}







@media (max-width: 767px) {
  .left_filter {
    width: 44%;
}
  .filters {
    padding: 0px;
   width: 100%;
    z-index: 222;
    position: fixed;
    bottom: 0;
    background-color: white;
  }

  .left_filter {
    border: 1px solid #000000ab;
  }
  .left_filter a {
    padding: 0px 21px;
    text-decoration: none;
    color: black;
    font-size: 11px;
    font-weight: bold;
  }
  .left_filter a svg {
    width: 15px;
  }
  .left_filter img {
    margin-left: 3px;
  }
  #shrot_by {
    margin: 0px 14px;
  }
}
</style>
