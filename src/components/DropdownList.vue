<template>
    <div class="dropdown w-100">
        <a v-for="item in itemList" :key="item.phrase + Math.random()" class="dropdown-item" href="#" @click="selectItem(item)">
        {{ item.phrase }}
        </a>
    </div>
</template>

<script>
export default {
    props: {
        itemList: Array
    },
    data() {
        return {
            selectedItem: {},
        }
    },
    methods: {
        selectItem(item) {
            this.selectedItem = item;
            this.$emit('on-item-selected', item)
        },
        resetItem() {
            this.selectedItem = {};
        }
    }
}
</script>

<style>

    .dropdown {
        background-color: #F6F3EE;
        border: 1px solid #D3CDB8;
        box-sizing: border-box;
        box-shadow: 0px 1px 14px rgba(0, 0, 0, 0.05);
        border-radius: 3px;
        overflow: scroll;
        padding: 16px 32px 16px 16px !important;
        max-height: 180px;
    }
    .dropdown-item {
        width:100%;
        background-color: inherit;
        margin: 4px 0px !important;
        border-radius: 1px !important;
        border:none;
        font-size: 14px;
        padding : 8px 0px 10px 14px;
        display: inline-flex;
        justify-content: start;
        cursor: pointer;
    }
    .dropdown-item:hover, .dropdown-item:focus {
        background-color: rgba(68, 68, 68, 0.1);
        outline: none;
    }
    ::-webkit-scrollbar {
        width: 36px;
    }
    ::-webkit-scrollbar-thumb {
        min-height: 70px;
        border: 16px solid rgba(0, 0, 0, 0);
        background-clip: padding-box;
        border-radius: 40px;
        -webkit-border-radius: 40px;
        background-color: #A9A9A9;
        box-shadow: inset -1px -1px 0px rgba(0, 0, 0, 0.05), inset 1px 1px 0px rgba(0, 0, 0, 0.05);
        -webkit-box-shadow: inset -1px -1px 0px rgba(0, 0, 0, 0.05), inset 1px 1px 0px rgba(0, 0, 0, 0.05);
    }
    ::-webkit-scrollbar-button {
        width: 0;
        height: 0;
        display: none;
    }
    ::-webkit-scrollbar-corner {
        background-color: transparent;
    }
</style>