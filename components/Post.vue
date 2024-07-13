<template>
    <div :class="'card' + (importante ? ' bg-importante' : ' bg-normal')">
        <div class="card-body">
            <div class="card-title">
            <div class="row justify-content-between">
                <div class="col-auto"><h5>{{ titulo }}</h5></div>
                <div class="col-auto"><button type="button" class="btn-close" aria-label="Close" v-on:click="remove()"></button></div>
            </div>
            </div>
            <p class="card-text">{{ desc }}</p>
        </div>
    </div>
</template>
<script setup lang="ts">
import {ref} from 'vue'; 

const props = defineProps({
    titulo: {type: String, required: true},
    desc: {type: String, required: true},
    importante: {type: Boolean, required: true}
});
const emit = defineEmits(["remove"]);

const remove = (i: number) => {
    emit("remove");
}
</script>
<style scoped>
  .bg-importante{
    background-color: #eb7061 !important;
  }
  .bg-normal{
    background-color: #fffecc !important;
  }
</style>