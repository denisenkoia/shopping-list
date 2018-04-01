<template>
    <div id="app" class="app">

        <div class="app-header">
            <div class="app-header-title">Shopping list</div>
            <div class="app-header-action">
                <base-btn v-if="selectedProduct.length" :icon="true" @click="submitSelect">
                    <i class="material-icons">done</i>
                    Submit
                </base-btn>
            </div>
        </div>

        <div class="shop-list-wrapper">
            <shop-list-item v-for="(item, index) of shopList" :key="index" :item="item"></shop-list-item>
        </div>

    </div>    
</template>



<script>
import ShopListItem from "./ShopListItem.vue";
import BaseBtn from "./BaseBtn.vue";

import API_SHOP_LIST from "../API/API_SHOP_LIST.json";

class shopListItem {
    constructor( item ) {
        this.ItemID = item.ItemID;
        this.GUID = item.GUID;
        this.Name = item.Name || null;
        this.imageUrl = item.imageUrl || null;
        this.Notes = item.Notes || null;
        this.DisplayQuantity = item.DisplayQuantity;
        this.Department = item.Department;
        this.IsChecked = item.IsChecked;
        this.Count = parseInt(item.DisplayQuantity);
        this.CountOperand = this.Count;
        this.Units = item.DisplayQuantity.match(/[a-zA-Z]/g).join('');
    }
    dicrementCount() {
        this.Count -= this.CountOperand;
    }
    incrementCount() {
        this.Count += this.CountOperand;
    }
}

export default {
    components: {
        ShopListItem,
        BaseBtn
    },
    data() {
        return {
            shopList: [],
        }
    },
    computed: {
        selectedProduct() {
            return this.shopList.filter( (item) => {
                if ( item.IsChecked ) {
                    return true;
                }
            })
        }
    },
    methods: {
        getShopList() {
            for (let item of API_SHOP_LIST.Items ) {
                this.shopList.push( new shopListItem(item) )
            }
        },
        submitSelect() {
            console.log( this.selectedProduct );
        }
    },
    created() {
        this.getShopList();
    }
};
</script>


<style lang="scss" scoped>

    .app-header {
        padding: 12px 16px;
        background: #27AE60;
        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.24);
        display: flex;
        align-items: center;
        justify-content: space-between;
        position: fixed;
        z-index: 2;
        width: 100%;
        left: 0;
        top: 0;
        .app-header-title {
            color: #fff;
            line-height: 18px;
        }
    }

    .app-footer {
        background-color: #fff;
        box-shadow: 0px -2px 4px rgba(0, 0, 0, 0.24);
        padding: 16px;
        display: flex;
        align-items: center;
        justify-content: center;
        position: fixed;
        z-index: 2;
        width: 100%;
        bottom: 0;
    }

    .shop-list-wrapper {
        margin-top: 42px; 
    }
    

    @media screen and (min-width: 1024px) {

        .shop-list-wrapper {
            max-width: 1000px;
            margin: 30px auto 0 auto;
            box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.24);
            border-radius: 2px;
        }
        .app-header {
            position: static;
        }

    }

</style>
