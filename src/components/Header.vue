<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled>Quis App</b-nav-item>
      <b-nav-item disabled>Counter :{{current}}/{{countQuestion}}</b-nav-item>
      
    </b-nav>
  </div>
</template>
<script>
export default {
  props:{
    countQuestion:Number,
    current:Number
  }
}
</script>

