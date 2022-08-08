<template>
  
    <div class="container">
      <div class="row">
        <div class="col-6">
         
        </div>
        <div class="col-6">
          <div class="icons">
           <div class="align-self-center">
            <button class="btn btn-legacy font-text btn-lg p-2 " id="uid2" data-action="modal" data-ym_goal=""
              data-ga_category="" data-ga_action="" data-modal="cart"><span class="text icon"><i
                  class="fa fa-shopping-cart"></i><span>(0)</span></span></button>
              </div>
          </div>
        </div>
      </div>
    </div>
   

</template>

<script>
import { menuList } from '../constants/menuLinks'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      headerMenuList: menuList,
    }
  },
}
</script>

<style lang = "scss">
@import '../assets/layouts/index';

.navbar {
  height: 90px;
}

.navbar-nav {
  height: 90px;
}

.logo {
  /*padding-right: 180px ;*/
  width: 75px;
  height: 75px;

}

.collapse-fontsize {
  font-size: 18px;
}

.menu-link {
  padding: 25px 19px;
}


.icons {
  a {
    width: 30px;
    height: 30px;
    text-align: center;
    border: 1px solid $greyLight;
    border-radius: 50%;
    margin-right: 10px;
    display: flex;
  }
}
</style>