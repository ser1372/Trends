<template>
<footer class = "footer footer_bg">
<div class="container">
    <div class="row">
        <FooterIcons/>
        
        <FooterClient :footerMenuClient = "footerMenuClient"/>
        <FooterContacts/>
    </div>

</div>
</footer>
</template>

<script>
import { menuList, menuClient } from  '../../constants/menuLinks'

import FooterIcons from './FooterIcons.vue';
import FooterClient from './FooterClient.vue';
import FooterContacts from './FooterContacts.vue';

export default{
    data() {
        return {
            footerMenu: menuList,
            footerMenuClient: menuClient,
        };
    },
    components: { FooterIcons,  FooterClient, FooterContacts }
}
</script>