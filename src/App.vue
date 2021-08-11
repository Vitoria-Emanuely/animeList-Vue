<template>
  <div id="container" class="container">
    <h1 class="mt-4">{{ titulo }}</h1>
    <div class="row">
      <div class=" mb-2 col-3">Nome do anime</div>
      <div class=" mb-2 col-3">Episódios assistidos /</div>
      <div id="title" class="mb-2 col-2">Episódios Totais</div>
      <div id="titleS" class="mb-2 col-3">Status</div>
    </div>
  <div class="row">
    <input v-model="anime.nome" class="col-3 ml-3 form-control" type="text" placeholder="Novo anime"> 
    <input v-model="anime.ep" class="form-control col-1 ml-4" type="number" @change="addStatus"> 
    <div class="ml-4 bar">/</div>
    <input v-model="anime.epT" class="form-control col-1 ml-4" type="number" @change="addStatus">

    <select class="form-control col-2 ml-3" v-model="anime.status" @change="addStatus">
      <option v-for="(status, index) in statusT" :key="index">{{ status }} </option>
    </select>
    <button @click="addAnime" class="btn btn-info ml-2">Adicionar</button>

  </div>
  <div class="row mt-4 ml-1" v-if="animes.length == 0">Nenhum Anime Cadastrado</div>
  <div v-else class="column">
    <div class="row" v-for="(anime, i) in animes" :key="i">
      
        <div class="mt-4 col-3 ml-1 mr-3">{{ anime.nome }}</div>
        <div class="mt-4 col-1 ml-5">{{ anime.ep }}</div>
        <div class="mt-3 bar space mr-1">/</div>
        <div class="mt-4 col-1 ml-5">{{ anime.epT }}</div>
        <div class="mt-4 col-1 ml-4 mr-3">{{ anime.status }}</div>
        <div class="mt-4 col-1 ml-5">
        <button @click="delAnime(i)" class="btn btn-info">Deletar</button>
        </div>
    </div>
  </div>
</div>
</template>

<script>

export default {
name: 'App',
  data() {
    return {
      titulo: "My AnimeList",
      anime: {
        nome: "",
        ep: "",
        epT: "",
        status: "",
      },
      animes: [
        { nome: "Uramichi Oniisan", ep: "5", epT: "13", status: "Assistindo" },
        { nome: "Tokyo Revengers", ep: "18", epT: "24", status: "Assistindo" },
      ],
      statusT: [
        "Quero assistir",
        "Completo",
        "Assistindo",
        "Desisti",
      ],
    }
  },
  methods: {
    addStatus() {
      if (this.anime.ep > 0) {
        this.anime.status = "Assistindo"
      }
      if (this.anime.ep == this.anime.epT){
        this.anime.status = "Completo"
      }
    },
    addAnime() {
      if (this.anime.ep > this.anime.epT) {
        alert("Digite um número de episódios assistidos válido!")
      }
      else if (this.anime.status == ""){
        alert("Selecione um status!")
      }
      else {
        this.animes.push({
          nome: this.anime.nome,
          ep: this.anime.ep,
          epT: this.anime.epT,
          status: this.anime.status,
        })
      }  
      this.anime.nome = ""
      this.anime.ep = ""
      this.anime.epT = ""
      this.anime.status = ""
    },
    delAnime(i) {
      this.animes.splice(i, 1)
    }
  }
}
</script>

<style> 
#container {
  min-width: 0;
  margin: 20px auto 0px auto;
}

.bar{
    font-size: 1.60em;
}

.space{
    margin-left: -0.5%;
}

#title{
    margin-left: -9.8%;
}

#titleS{
    margin-left: -5.8%;
}

</style>
