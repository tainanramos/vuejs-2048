<template>
<input type="text"  
  @keydown.left="this.$emit('leftPress')"
  @keydown.right="this.$emit('rightPress')"
  @keydown.down="this.$emit('downPress')"
  @keydown.up="this.$emit('upPress')"
  autofocus>
  <div class="matriz" @click="this.$emit('startGame')">
    <div class="linha" v-for="(linha, i) in mat" :key="i">
      <div class="coluna" v-for="(coluna, x) in linha" :key="x">
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
};
</script>

<style>
.matriz{
  border: 1px solid #ddd;  
  width: 200px;
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
  border: 1px solid #ddd;
  width: 50px;
  height: 50px;
}
</style>