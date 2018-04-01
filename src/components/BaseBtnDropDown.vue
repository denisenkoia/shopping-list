<template>
    <div class="b-btn-dropdown-wrap">
        <button :class="{'open' : openProp}" @click="$emit('click')">
            <i class="material-icons">keyboard_arrow_down</i>
        </button>
    </div>
</template>


<script>

export default {
    props: {
        openProp: {
            type: Boolean,
            default: false
        }
    },
};

</script>


<style lang="scss" scoped>

.b-btn-dropdown-wrap {
    button {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 30px;
        height: 30px;
        border-radius: 50%;
        overflow: hidden;
        cursor: pointer;
        &.open {
           .material-icons {
               transform: rotateX(180deg);
           } 
        }
        .material-icons {
            font-size: 20px;
            color: #9E9E9E;
            transition-property: transform;
            transition-duration: 0.3s;
        } 
    }
}
</style>
