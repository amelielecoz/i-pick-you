<template>
    <span class="input d-inline" :class="className">{{ content }}</span>
</template>
<script>
export default {
    props: {
        content: String,
        className: String
    }
}
</script>
<style scoped>
    .input {
        font-style: normal;
        font-weight: normal;
        font-size: 26px;
        padding-left: 2px;
        padding-right: 2px;

    }
    .user-name {
        color: #444444;
    }
    .keyword {
        color: #525edd;
        margin-right:6px;
    }
    .pokemon-name {
        background: rgba(68, 68, 68, 0.1);
        border-radius: 3px;
        padding: 2px 10px;
        font-weight: 500;
        font-size: 22px;
        color: #444444;
    }

</style>