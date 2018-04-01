<template>
    <div class="b-checkbox-wrap">
        <label :class="{'checked' : value}">
            <input type="checkbox" :checked="value" @change="$emit('input', $event.target.checked)">
            <i v-show="value" class="material-icons">done</i>
        </label>
    </div>
</template>


<script>

export default {
    props: {
        value: {
            type: Boolean,
            default: false
        }  
    }
};

</script>


<style lang="scss" scoped>

    .b-checkbox-wrap {
        input {
            display: none;
        }
        label {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 34px;
            height: 34px;
            position: relative;
            cursor: pointer;
            &:before {
                content: "";
                display: inline-block;
                width: 18px;
                height: 18px;
                position: absolute;
                border: 2px solid #9E9E9E;
                border-radius: 2px;
                left: 8px;
                top: 8px;
            }
            &.checked {
                &:before {
                    border: 1px solid #27AE60;
                    background-color: #27AE60;
                }  
            }
            .material-icons {
                position: relative;
                color: #ffffff;
                font-size: 18px;
            }
        }
    }

</style>