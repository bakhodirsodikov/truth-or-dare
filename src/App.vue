<template>
<div class="container main-container">
  <button class="btn btn-outline-info rounded-circle info"
  v-if="!info"
  @click="info = true"
  >?</button>
  <div class="info-text d-flex flex-column"
  v-if="info">
    <span class="w-100 d-flex justify-content-end">
      <button class="btn btn-outline-danger close-info"
      @click="info = false">
        X
      </button>
    </span>
    <h3 class="text-center">Добро пожаловать в игру "Правда или действие"</h3>
    <ul v-for="(info, idx) in infoText"
    :key="idx">
      <h4 class="text-center"> {{ info.title }} </h4>
      <li v-for="text in info.text"
      :key="text.id"> {{ text }} </li>
    </ul>
  </div>
  <div v-if="!info">
    <div class="greetings d-flex flex-column align-items-center"
    v-if="display">
      <h1 class="text-center">{{ firstGreating }}</h1>
      <div class="w-100 d-flex flex-column flex-md-row justify-content-md-center">
        <div class="players m-3 text-center"
        v-for="(player,  idx) in players"
        :key="player.id"
        >{{player.which}}: {{ idx + 1 }}
          <input type="text"
          class="ps-1 input"
          v-model="player.name"
          >
          <p class="text-danger"
          >  {{player.error}}</p>
        </div>
        
      </div>
      
      <div class="dropdown">
        <p class="fs-5 text-danger text-center m-0"
        v-if="ruleError"> {{ ruleError }} </p>
        <button class="btn btn-info dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false">
          {{ selected }}
        </button>
        <ul class="dropdown-menu w-100">
          <li class="dropdown-item"
          v-for="(rule, idx) in rules"
          :key="idx"
          @click="selected = rule.name"
          >{{ rule.name }}</li>
        </ul>
      </div>
      <button type="button" 
      class="btn btn-outline-success my-5 get-start"
      @click="getStart">
      <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" fill="currentColor" class="bi bi-triangle" viewBox="0 0 16 16">
        <path d="M7.938 2.016A.13.13 0 0 1 8.002 2a.13.13 0 0 1 .063.016.146.146 0 0 1 .054.057l6.857 11.667c.036.06.035.124.002.183a.163.163 0 0 1-.054.06.116.116 0 0 1-.066.017H1.146a.115.115 0 0 1-.066-.017.163.163 0 0 1-.054-.06.176.176 0 0 1 .002-.183L7.884 2.073a.147.147 0 0 1 .054-.057zm1.044-.45a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566z"/>
      </svg>
      </button>
  
    </div>
    <div class="main d-flex flex-column w-100 align-items-center" v-if="!display">
      <h1 v-if="step == 0"> {{ forPlayer }} </h1>
      <h1 v-if="step > 0">  {{ nextStep }} </h1>
      <button 
      v-if="step < 30"
      class="btn btn-outline-success my-3 fs-3"
      @click="step = step + 1">
        next
        <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class="bi bi-arrow-right" viewBox="0 0 16 16">
          <path fill-rule="evenodd" d="M1 8a.5.5 0 0 1 .5-.5h11.793l-3.147-3.146a.5.5 0 0 1 .708-.708l4 4a.5.5 0 0 1 0 .708l-4 4a.5.5 0 0 1-.708-.708L13.293 8.5H1.5A.5.5 0 0 1 1 8z"/>
        </svg> 
      </button>
      <div class="restart-container w-100 d-flex justify-content-end">
        <button class="btn btn-outline-primary"
        @click="display = true, firstGreating = '', selected = 'Виберите подходящую тему для игры 🙃', step = 0">
          <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class="bi bi-arrow-clockwise" viewBox="0 0 16 16">
            <path fill-rule="evenodd" d="M8 3a5 5 0 1 0 4.546 2.914.5.5 0 0 1 .908-.417A6 6 0 1 1 8 2v1z"/>
            <path d="M8 4.466V.534a.25.25 0 0 1 .41-.192l2.36 1.966c.12.1.12.284 0 .384L8.41 4.658A.25.25 0 0 1 8 4.466z"/>
          </svg>
        </button>
      </div>
    </div>
  </div>

  <footer>
    <p>Все вопросы и действия сгенирированы с помощью ChatGPT</p>
  </footer>
</div>
</template>

<script src="./main.js"></script>

<style src="../node_modules/bootstrap/dist/css/bootstrap.css">
</style>
<style src="./app.css">

</style>

