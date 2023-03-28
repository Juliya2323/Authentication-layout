<template>
    <button>
        <slot></slot>
    </button>
</template>

<style scoped>
button {
    display: block;
    background-color: #7F56D9;
    width: 100%;
    color: white;
    padding-top: 10px;
    padding-bottom: 10px;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #9677db;
}
</style>