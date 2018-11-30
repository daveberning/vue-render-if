<template>
  <div class="hello">
    <render-if :defined="technology">
      <p>You should see me!</p>
    </render-if>
  </div>
</template>

<script>
import RenderIf from '../../src/RenderIf';

export default {
  components: {
    RenderIf
  },
  data() {
    return {
      technology: 'Vue.js'
    }
  }
}
</script>