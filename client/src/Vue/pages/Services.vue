<template>
  <section id="services" class="light-section">
    <div class="container-fluid">
      <h1 class="section-header">{{ heading }}</h1>

      <!-- start of filters  -->
      <div class="row filters">
        <ul
          class="list-inline mx-auto"
          data-aos="fade-right"
          data-aos-duration="1000"
        >
          <li
            v-for="item in services"
            :key="item.category"
            class="list-inline-item filter"
          >
            <a
              class="nav-item"
              :class="item.category === currentCategory ? 'active' : null"
              :data-category="item.category"
              @click="setCategory"
              >{{ item.category }}</a
            >
          </li>
        </ul>
      </div>
      <!-- end of filters  -->

      <!-- start of service container  -->
      <div
        id="service-container"
        data-aos="fade-right"
        data-aos-duration="1000"
        v-for="item in filteredServices"
        :key="item.category"
      >
        <div class="category-heading">
          <h2><i :class="item.faClass"></i> {{ item.category }}</h2>
          <h3 :v-if="item.subtitle !== ''">{{ item.subtitle }}</h3>
        </div>

        <div class="service-content">
          <!-- start of service bars  -->
          <div v-if="item.packets.length !== 0" class="servicebars">
            <div
              class="service"
              v-for="service in item.packets"
              :key="service.name">
              <h2 class="service-name" v-html="service.name"></h2>
              <h6 v-html="service.description"></h6>
              <h5 class="price">{{service.price}} {{service.currency}}</h5>
            </div>
          </div>
          <!-- end of service bars  -->
        </div>
      </div>
      <!-- end of service container  -->
    </div>
    <!-- end of main container  -->
    <Arrow />
  </section>
</template>

<script>
import data from "../../data/data.json";
import Arrow from "../components/Arrow.vue";

export default {
  name: "Services",
  props: {},
  components: {
    Arrow,
  },
  data() {
    return {
      services: data.services.categories,
      heading: data.main.headings.services,
      currentCategory: data.services.defaultCategory,
    };
  },
  computed: {
    filteredServices() {
      var services = data.services.categories;
      var category = this.currentCategory;
      var filtered = services.filter(function(x) {
        if (x.category === category) {
          return x;
        }
      });

      console.log(filtered);

      return filtered;
    },
  },
  methods: {
    setCategory(event) {
      this.currentCategory = event.target.dataset.category;
    },
  },
};
</script>

<style lang="scss"></style>
