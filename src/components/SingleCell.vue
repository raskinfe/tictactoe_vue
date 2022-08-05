<template>
    <div class="cell">{{this.value}}</div>
</template>
<script>
export default {
    name: 'SingleCell',
    props: {
        value:{
            type: String,
            default() {
                return "";
            },
        }
    }}
</script>
<style scoped>
.cell {
    border: 2px solid #fff;
    min-width: 150px;
    min-height: 100px;
    display: flex;
    justify-content: center;
    align-content: center;
    align-items: center;
    color: #fff;
    font-size: 40px;
    cursor: pointer;
}
.cell:hover{
    background: rgb(238, 221, 221);
    color: #000;
    transform: scale(1.03);
    border-radius: 10px;
}
</style>