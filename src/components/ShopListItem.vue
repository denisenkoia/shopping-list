<template>
    <div class="s-list-item">

        <div class="s-item-header">
            <base-checkbox v-model="item.IsChecked"></base-checkbox>
            <div class="s-item-title" v-if="item.Name">{{item.Name}}</div>
            <div class="s-item-header-action">
                <base-btn class="green" :disabled="item.Count <= 0" :circle="true" @click="item.dicrementCount()">
                    <i class="material-icons">remove</i>
                </base-btn>
                <div class="s-item-count">
                    {{ item.Count }}<br>{{ item.Units }}
                </div>
                <base-btn class="green" :circle="true" @click="item.incrementCount()">
                    <i class="material-icons">add</i>
                </base-btn>
                <base-btn-drop-down @click="toogleBody" :openProp="bodyOpen"></base-btn-drop-down>
            </div>
        </div>

        <transition @enter="enter" @leave="leave">
            <div class="s-item-body-wrapper" v-show="bodyOpen">
                <div class="s-item-body">
                    <img v-if="item.imageUrl" :src="item.imageUrl" alt="img">
                    <p v-if="item.Notes" class="s-item-desc">{{ item.Notes }}</p>
                </div>
            </div>
        </transition>
            
    </div>
</template>

<script>
import Velocity from "velocity-animate";
import BaseBtn from "./BaseBtn.vue";
import BaseBtnDropDown from "./BaseBtnDropDown.vue";
import BaseCheckbox from "./BaseCheckbox.vue";

export default {
    props: {
        item: {
            type: Object,
            default: {}
        }
    },
    components: {
        BaseBtn,
        BaseCheckbox,
        BaseBtnDropDown
    },
    data() {
        return {
            bodyOpen: false
        };
    },
    methods: {
        toogleBody() {
            this.bodyOpen = !this.bodyOpen;
        },
        enter(el, done) {
            Velocity(el, "slideDown", { duration: 500 });
        },
        leave(el, done) {
            Velocity(el, "slideUp", { duration: 500 }, { complete: done });
        }
    }
};
</script>

<style lang="scss" scoped>

.s-list-item {
    border-bottom: 1px solid #E0E0E0;
    .s-item-header {
        display: flex;
        align-items: center;
        padding: 8px;
        .s-item-prew {
            height: 35px;
            width: 35px;
            margin-left: 15px;
            img {
                height: 100%;
                width: 100%;
            }
        }
        .s-item-title {
            margin-left: 8px;
            font-size: 15px;
            color: #212121;
            flex: 1;
        }
        .s-item-header-action {
            display: flex;
            align-items: center;
            .s-item-count {
                width: 42px;
                font-size: 13px;
                line-height: 1.2;
                text-align: center;
                position: relative;
                color: #757575;
            }
            .s-item-units {
                font-size: 15px;
                position: absolute;
                top: 25px;
                left: 50%;
                transform: translateX(-50%);
            }
            .b-btn-dropdown-wrap {
                margin-left: 20px;
            }
        }
    }
    .s-item-body {
        padding: 0 16px 12px;
        p {
            font-size: 12px;
            line-height: 15px;
            color: #4F4F4F;
        }
        img {
            width: 100%;
            margin-bottom: 12px;
        }
    }
}

@media screen and (min-width: 1024px) {

    .s-list-item {
       .s-item-body {
           display: flex;
           align-items: flex-start;
            p {
                font-size: 14px;
                line-height: 20px; 
            }
            img {
                width: 400px;
                margin-right: 16px;
                margin-bottom: 0;
            }
        } 
    }
    
}

</style>

