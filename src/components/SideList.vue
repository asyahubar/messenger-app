<template>
    <div id="side-list">
        <p>bob123</p>
    </div>
</template>

<script>
    export default {
        name: 'SideList',
    }
</script>

<style lang="scss">
    #side-list {
        width: 250px;
        height: 100vh;
        background-color: #1c1c1c;
        display: inline-block;

        p {
            box-sizing: content-box;
            padding: 10px 16px;
            color: royalblue;
            background-color: #2f2f2f;
        }
    }
</style>