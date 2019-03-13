<template>
    <label class="vue-switch"
        :class="[{ 'checked': value, 'disabled': disabled }]">
        <input class="checkbox"
            type="checkbox"
            v-model="checked"
            @change="$emit('input', checked)"
            :disabled="disabled || readonly"
            :checked="value">
    </label>
</template>

<script>
export default {
    name: 'VueSwitch',

    props: {
        disabled: {
            type: Boolean,
            default: false,
        },
        readonly: {
            type: Boolean,
            default: false,
        },
        value: {
            type: [Boolean, Number],
            default: false,
            required: true,
        },
    },

    data: v => ({
        checked: v.value,
    }),

    watch: {
        value(value) {
            this.checked = value;
        },
    },
};
</script>

<style lang="scss">
    .vue-switch {
        --height: 1rem;

        background-color: #dbdbdb;
        border: 1px solid #dbdbdb;

        &:before {
            background-color: #b5b5b5;
        }

        &:after {
            background-color: #fff;
        }

        input {
            opacity: 0;
            display: inline-flex;
            width: 100%;
            height: 100%;
        }

        position: relative;
        border-radius: var(--height);
        width: calc(1.625 * var(--height));
        height: var(--height);
        cursor: pointer;
        display: inline-flex;
        vertical-align: middle;
        align-items: center;
        justify-content: center;

        &:before,
        &:after {
            content: ' ';
            position: absolute;
            top: 0;
            left: 0;
            height: calc(var(--height) - 2px);
            border-radius: var(--height);
            transition: 0.25s;
        }

        &:before {
            width: calc(1.625 * var(--height) - 2px);
        }

        &:after {
            width: calc(var(--height) - 2px);
            background-color: #fff;
            box-shadow: 0 2px 3px rgba(17, 17, 17, 0.1);
        }

        &.checked {
            border-color: #4a4a4a;
            background-color: #4a4a4a;
            &:before {
                transform: scale(0);
            }
            &:after {
                transform: translateX(calc(0.625 * var(--height)));
            }
        }

        &.is-small {
            --height: 0.75rem;
        }
        &.is-medium {
            --height: 1.25rem;
        }
        &.is-large {
            --height: 1.5rem;
        }
    }
</style>
