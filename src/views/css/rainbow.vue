<template>
  <ul class="inlinelist">
    <li v-for="item in languages" :key="item.language" class="inlinelist-item">
      <a href="#">
        {{ item.language }}
        <code>*.{{ item.suffix }}</code>
      </a>
    </li>
  </ul>
</template>

<script setup>
  const languages = [
    { language: 'HTML', suffix: 'html' }
  ]
</script>

<style scoped lang="scss">
@keyframes rainbow {
  0% {
    background-position: 0 50%
  }

  100% {
    background-position: 100% 50%
  }
}

.inlinelist {
  &-item {
    display: inline;
    box-decoration-break: clone;
    white-space: normal;
    padding: 0.2em 0.5em;
    margin: 4px 4px 4px 0;
    transition: .15s linear outline;
    font-size: 100%;
    line-height: 2;
    background-color: #e9e9e9;

    &:hover {
      position: relative;
      background-image: linear-gradient(238deg,red,#ff8000,#ff0,#80ff00,#0f0,#00ff80,#0ff,#0080ff,#00f,#8000ff,#ff0080);
      background-size: 1200% 1200%;
      background-position: 2% 80%;
      color: #fff;
      text-shadow: 0 0 2px rgb(0 0 0 / 90%);
      animation: rainbow 4s ease-out alternate infinite;
    }

    a {
      color: #fff;
      text-decoration: none;
    }

    code {
      background-color: transparent;
      font-size: 80%;
      margin-left: 6px;
      padding-left: 6px;
      display: inline-block;
      position: relative;

      &::before {
        content: " ";
        border-left: 1px solid rgb(255 255 255 / 80%);
        position: absolute;
        left: -2px;
        top: -2px;
        bottom: 2px;
      }
    }
  }
}
</style>
