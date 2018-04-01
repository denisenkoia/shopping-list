<template>
    <div class="b-btn-wrap" @click="clickHandler">
        <button :disabled="disabled" :class="{'b-btn__circle' : circle, 'b-btn__icon' : icon}">
            <slot></slot>
        </button>
    </div>
</template>


<script>

export default {
    props: {
        disabled: {
            type: Boolean,
            default: false
        },
        circle: {
            type: Boolean,
            default: false
        },
        icon: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        clickHandler() {
            if ( !this.disabled ) {
                this.$emit('click');
            }
        }
    }
};

</script>


<style lang="scss" scoped>

@mixin color ( $bgColor ) {
    button {
        background-color: $bgColor;
    }
}

.b-btn-wrap {
    position: relative;
    &.green {
        @include color( #27AE60 );
    }
    .material-icons {
        font-size: 18px;
        color: #ffffff;
    }
    button {
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 2px;
        color: #ffffff;
        font-size: 14px;
        line-height: 18px;
        letter-spacing: 3%;
        text-transform: uppercase;
        position: relative;
        z-index: 1;
        cursor: pointer;
        &:disabled {
            background-color: #D6D6D6;
            cursor: default;
        }
        &.b-btn__circle {
            border-radius: 50%;
            width: 20px;
            height: 20px;
            overflow: hidden;
        }
        &.b-btn__icon {
            .material-icons {
               margin: 0 3px;
            } 
        }
    }
}
</style>