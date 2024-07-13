<template>
  <div class="container ">
    <div class="row">
      <div class="col-auto"><h1>Post It Simulator</h1></div>
    </div>
    <div class="row justify-content-center">
      <div class="col-sm-auto"><input type="text" class="form-control" placeholder="Título" v-model="titulo"></div>
      <div class="col-sm-auto"><input type="text" class="form-control" placeholder="Descripcion" v-model="desc" ></div>
      <div class="col-sm-auto"><div class="form-check">
          <input class="form-check-input" type="checkbox" value="" id="formCheckDefault" v-model="select_importante">
          <label class="form-check-label" for="formCheckDefault">Importante</label>
        </div>
      </div>
      <div class="col-sm-auto"><button type="button" class="btn btn-primary" v-on:click.prevent="addPost()">Agregar</button></div>
    </div>
      <div class="row row-cols-4 row-cols-md-4 g-4 mt-2">
        <div class="col" v-for="(item, i) in posts" :key="i">
          <div :class="'card' + (item.importante ? ' bg-importante' : ' bg-normal')">
            <div class="card-body">
              <div class="card-title">
                <div class="row justify-content-between">
                  <div class="col-auto"><h5>{{ item.titulo }}</h5></div>
                  <div class="col-auto"><button type="button" class="btn-close" aria-label="Close" v-on:click="remove(i)"></button></div>
                </div>
              </div>
              <p class="card-text">{{ item.desc }}</p>
            </div>
          </div>
        </div>
    </div>
  </div>
</template>
<script setup>
import { ref} from 'vue';

const titulo = ref("");
const desc = ref("");
const select_importante = ref(false);
const posts = ref([]);

const addPost = () => {
  posts.value.push(
    {
      "titulo": titulo.value,
      "desc" : desc.value,
      "importante" : select_importante.value
    });
  limpiar();
}

const limpiar = () => {
  titulo.value = "";
  desc.value = "";
  select_importante.value = "";
}

const remove = (i) => {
  posts.value.splice(i, 1);
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
