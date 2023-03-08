<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>

<style scoped>
button{
    color: white;
    background: black;
}

button:hover{
    color:  black;
    background: white;
    border: 1px solid black;
}
</style>