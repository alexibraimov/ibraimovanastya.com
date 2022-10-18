<template>
  <section id="portfolio" class="dark-section">
    <div class="container-fluid">
      <h1 class="section-header">{{ heading }}</h1>
      <div class="row filters">
        <ul class="list-inline mx-auto">
          <li v-for="item in filters" :key="item.title" class="list-inline-item filter">
            <a class="nav-item" :class="item.filter === currentFilter ? 'active' : null" :data-filter="item.filter" @click="setFilter">
              {{ item.filter }}
            </a>
          </li>
        </ul>
      </div>
      
      <div id="portfolio-container" class="row">
        <div data-aos="fade-right" data-aos-duration="1000" v-for="(item, index) in filteredProjects" :key="index" class="col-sm-12 col-md-4 flex-col">
          <div v-if="item.isBefore" class="portfolio-item">
            <BeforeAfter :value="50" :beforeImage="require(`../../assets/images/portfolio/${item.folder}/${item.image}`)" 
                                     :afterImage="require(`../../assets/images/portfolio/${item.folder}/before/${item.image}`)"/>
          </div> 
          <div v-else class="portfolio-item">
            <img :src="require(`../../assets/images/portfolio/${item.folder}/${item.image}`)"/>
          </div>
        </div>
      </div>
    </div> 
    <Arrow />
  </section>
</template>

<script>
import data from "../../data/data.json";
import Arrow from "../components/Arrow.vue";
import BeforeAfter from  "../components/BeforeAfter.vue";

export default {
  name: "portfolio",
  props: {},
  components: {
    Arrow,
    BeforeAfter,
  },
  data() {
    
    return {
      projects: data.portfolio.projects,
      heading: data.main.headings.portfolio,
      currentFilter: data.portfolio.defaultFilter
    };
  },
  computed: {
    filteredProjects() {
      var projects = data.portfolio.projects;
      var filter = this.currentFilter;
      var filtered = projects.filter(function(x) {
        return x.filter === filter;
      });
      return filtered;
    },
    filters() {
      var filterList = [];
      var projects = data.portfolio.projects;
      filterList = projects.filter(function(x) {
        if (!filterList.includes(x.filter)) {
          filterList.push(x.filter);
          return x.filter;
        }
      });
      return filterList;
    },
  },
  methods: {
    setFilter(event) {
      this.currentFilter = event.target.dataset.filter;
    },
  },
};
</script>

<style lang="scss"></style>
