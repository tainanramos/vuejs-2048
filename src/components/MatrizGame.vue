<template>
  <input
    type="text"
    @keydown.left="$emit('leftPress')"
    @keydown.right="$emit('rightPress')"
    @keydown.down="$emit('downPress')"
    @keydown.up="$emit('upPress')"
    autofocus
  />
  <div class="matriz" id="grid-game">
    <div class="linha" v-for="(linha, i) in mat" :key="i">
      <div
        class="coluna"
        v-for="(coluna, x) in linha"
        :key="x"
        :class="classItem(coluna)"
      >
        {{ coluna }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    mat: { type: Array, required: true },
  },
  emits: ["leftPress", "rightPress", "downPress", "upPress"],
  methods: {
    teste() {
      console.log("teste teste");
    },
    classItem(coluna) {
      let classItem;
      switch (coluna) {
        case 2:
          classItem = "cls-2";
          break;
        case 4:
          classItem = "cls-4";
          break;
        case 8:
          classItem = "cls-8";
          break;
        case 16:
          classItem = "cls-16";
          break;
        case 32:
          classItem = "cls-32";
          break;
        case 64:
          classItem = "cls-64";
          break;
        case 128:
          classItem = "cls-128";
          break;
        case 256:
          classItem = "cls-256";
          break;
        case 512:
          classItem = "cls-512";
          break;
        case 1024:
          classItem = "cls-1024";
          break;
        case 2048:
          classItem = "cls-2048";
          break;
        default:
          classItem = "cls-default";
          break;
      }
      return classItem;
    },
  },
};
</script>

<style>
.matriz {
  border: 2px solid rgb(186, 172, 159);
  width: 400px;
  user-select: none;
}
.linha {
  display: flex;
  justify-content: center;
}
.coluna {
  display: flex;
  text-align: center;
  justify-content: center;
  flex-direction: column;
  font-size: 2rem;
  font-weight: 600;
  border: 2px solid rgb(186, 172, 159);
  color: rgb(252, 243, 224);
  width: 100px;
  height: 100px;
}
.coluna.cls-default {
  background-color: rgb(204, 192, 179);
}
.coluna.cls-2 {
  background-color: rgb(238, 228, 218);
  color: rgb(117, 111, 91);
}
.coluna.cls-4 {
  background-color: rgb(236, 224, 200);
  color: rgb(117, 111, 91);
}
.coluna.cls-8 {
  background-color: rgb(239, 178, 124);
}
.coluna.cls-16 {
  background-color: rgb(243, 150, 106);
}
.coluna.cls-32 {
  background-color: rgb(243, 125, 99);
}
.coluna.cls-64 {
  background-color: rgb(246, 94, 69);
}
.coluna.cls-128 {
  background-color: rgb(234, 207, 118);
}
.coluna.cls-256 {
  background-color: rgb(238, 202, 105);
}
.coluna.cls-512 {
  background-color: rgb(236, 200, 90);
}
.coluna.cls-1024 {
  background-color: rgb(231, 194, 87);
}
.coluna.cls-2048 {
  background-color: rgb(231, 191, 78);
}
</style>