<template>
    <div class="container-fluid">
        <div class="details">
            <slot></slot>
        </div>
    </div>
</template>

<style scoped>
.container-fluid {
    padding: 0px;
    border-radius: 12px;
    box-shadow: 0 0px 8px rgba(0, 0, 0, 0.26);
    margin: 30px 0px 30px 0px
}
</style>