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
          <Post :titulo="item.titulo" :desc="item.desc" :importante="item.importante" v-on:remove="remove(i)" />
        </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref, reactive} from 'vue';

interface Titulo {
  titulo: string,
  desc: string,
  importante: boolean
}

const titulo = ref <string>("");
const desc = ref <string>("");
const select_importante = ref<boolean>(false);
const posts = reactive<Titulo[]>([]);

const addPost = () => {
  posts.push(
    {
      titulo: titulo.value,
      desc : desc.value,
      importante : select_importante.value
    });
  limpiar();
}

const limpiar = () => {
  titulo.value = "";
  desc.value = "";
  select_importante.value = false;
}

const remove = (i: number) => {
  posts.splice(i, 1);
}

</script>