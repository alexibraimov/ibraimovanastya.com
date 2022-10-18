<template>
  <footer class="footer section-dark font-small text-center">
    <ul class="list-inline">
      <li class="list-inline-item">
        <a class="nav-item nav-link active" href="#">
          Home
        </a>
      </li>
      <li class="list-inline-item">
        <a class="nav-item nav-link" href="#about">О себе</a>
      </li>
      <li class="list-inline-item">
        <a class="nav-item nav-link" href="#services">Услуги</a>
      </li>
      <li class="list-inline-item">
        <a class="nav-item nav-link" href="#portfolio">Портфолио</a>
      </li>
      <li class="list-inline-item">
        <a class="nav-item nav-link" href="#contact">Контакты</a>
      </li>
    </ul>

    <ul class="list-inline">
      <li
        v-for="(item, i) in social"
        :key="i"
        class="social-item list-inline-item"
      >
        <a :href="item.url" :alt="item.name">
          <i :class="item.faClass"> </i>
        </a>
      </li>
    </ul>

    <div class="copyright">
      <p>
        Copyright © {{ new Date().getFullYear() }}
        {{ text.main.name.first }} {{ text.main.name.last  }}.
        {{ text.footer.copyrightText }}
      </p>
    </div>
  </footer>
</template>

<script>
import data from "../../data/data.json";

export default {
  name: "Footer",
  components: {},
  props: {},
  data() {
    return {
      text: data,
      social: data.contact.social,
    };
  },
};
</script>

<style lang="scss"></style>
