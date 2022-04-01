<template>
    <div>
        <div class="filters">
      <div class="left_filter"  >
        <h3><svg xmlns="http://www.w3.org/2000/svg" width="18.467" height="11.654" viewBox="0 0 18.467 11.654">
            <g transform="translate(-1149.5 42.429)">
              <rect width="8.992" height="1.869" transform="translate(1149.5 -40.656)" />
              <rect width="3.932" height="1.869" transform="translate(1164.035 -40.656)" />
              <rect width="8.992" height="1.869" transform="translate(1167.967 -32.406) rotate(-180)" />
              <rect width="3.932" height="1.869" transform="translate(1153.432 -32.406) rotate(-180)" />
              <rect width="1.74" height="5.35" transform="translate(1160.393 -42.429)" />
              <rect width="1.74" height="5.35" transform="translate(1154.987 -36.124)" />
            </g>
          </svg>SHOW FILTER</h3>
      </div>
      <div class="hide">
        <a href=""><svg xmlns="http://www.w3.org/2000/svg" width="18.467" height="11.654" viewBox="0 0 18.467 11.654">
            <g transform="translate(-1149.5 42.429)">
              <rect width="8.992" height="1.869" transform="translate(1149.5 -40.656)" />
              <rect width="3.932" height="1.869" transform="translate(1164.035 -40.656)" />
              <rect width="8.992" height="1.869" transform="translate(1167.967 -32.406) rotate(-180)" />
              <rect width="3.932" height="1.869" transform="translate(1153.432 -32.406) rotate(-180)" />
              <rect width="1.74" height="5.35" transform="translate(1160.393 -42.429)" />
              <rect width="1.74" height="5.35" transform="translate(1154.987 -36.124)" />
            </g>
          </svg>HIDE FILTER</a>
      </div>
      <div class="right_filter">
        <select name="shrot_by" id="shrot_by">
          <option value="short">SHORT BY</option>
        </select>
        <div class="shrot_by_choice">
                <ul>
                  <li><a href="#"> Price: Low to High</a></li>
                  <li><a href="#"> Price: High to Low</a></li>
                  <li><a href="#"> Discount</a></li>
                  <li><a href="#"> Popularity</a></li>
                  <li><a href="#"> Newest</a></li>
                </ul>

        </div>
    </div>
  </div>
    </div>
</template>
<script>
export default{
    name: 'Filter',
    props:{
      productFilter:Array,
    }

}


</script>
<style scoped>
.filters {
  display: flex;
  justify-content: space-between;
  padding: 23px;
}
#shrot_by {
  font-family: "Jost* 500";
  padding: 12px 30px;
  border-radius: 0px;
}
.shrot_by_choice{
display: none;
  position: absolute;
  z-index: 1;
  border: 1px solid;
  background-color: white;
}
.shrot_by_choice ul li{

  list-style: none;
  margin: 14px 4px;
}

.shrot_by_choice ul li a{
  margin: 16px 6px;
  text-decoration: none;
  color: #303030;
}
.hide{
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
.products_div{

    margin: auto;
    justify-content: space-between;
    display: flex;
    flex-wrap: wrap;
    
}
.side_filter{
  width: 100%;
  display: none;
 
  transform: translateX(-20vw);
  transition: all 0.5s ease-in-out;
}
.side_filter h3{
  font-size: 16px;
  font-weight: 100;
  padding: 13px 0px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid;
  width: 76%;
}
.side_filter ul li{
  padding: 10px;
}
.filter_type_list{
  display: none;
}
.filter_type_list_display{
  display: block;
}
@media (max-width: 767px){
   .filters {
    display: flex;
    padding: 0;
    width: 100%;
       z-index: 1;
    position: fixed;
    bottom: 0;
    background-color: white;
    justify-content: space-evenly;
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