<template>
  <section id="contact" class="light-section">
    <div class="container-fluid">
      <h1 class="section-header">{{ heading }}</h1>
      <div class="row">
        <div
        class="col-sm-12 col-md-6 flex-col"
        data-aos="fade-right"
        data-aos-duration="1000"
        style="margin: 0 auto;"
        >
        <div class="contact-content">
          <div class="contact-text">{{ contact.text }}</div>
          
          <div class="contact-info">
            <ul class="list-group list-group-flush">
              <li v-if="contact.city !==''" class="list-group-item">
                <h3 class="d-inline">
                  <i class="fas fa-map-marker-alt"></i> Локация:
                </h3>
                <br class="d-md-none" />
                <span>&nbsp; {{ contact.city }}</span>
              </li>

              <li class="list-group-item" v-if="contact.email !==''">
                <h3 class="d-inline">
                  <i class="fa fa-envelope"></i> Email:
                </h3>
                <a :href="'mailto:'+ contact.email">{{ contact.email }}</a>
              </li>
              
              <li class="list-group-item" v-if="contact.phone !==''">
                <h3 class="d-inline">
                  <i class="fas fa-phone"></i>  Номер:
                </h3>
                <br class="d-md-none" />
                
                <span>{{ contact.phone }}</span>
                
              </li>
              <li class="list-group-item">
                  <h3 class="d-inline">
                    <i class="fas fa-user-plus"></i> Соц сети:
                  </h3>
                  <br class="d-md-none" />

                  <div
                    v-for="(item, i) in social"
                    :key="i"
                    class="social-item social-spacing list-inline-item"
                  >
                    <a :href="item.url" :alt="item.name">
                      <i :class="'fa-lg '+item.faClass"> </i>
                    </a>
                  </div>
                </li>
          </ul>
        </div>
      </div>
    </div>
    <div
    class="col-sm-12 col-md-6 flex-col"
    data-aos="fade-right"
    data-aos-duration="1000"
    v-if="contact.form"
    
    >
    <h2 v-if="contact.formTitle !==''">{{contact.formTitle}}</h2>
    
    <div class="container contact-form">
      <form :action="contact.formEndPoint" method="GET" target="_blank">
        <div class="form-group">
          <textarea v-model="text" class="form-control" id="message" rows="5" placeholder="Введите сообщение" required></textarea>
        </div>
            <button v-if="text" class="btn"  v-on:click="btnClick(text)">
              <i class="fa fa-paper-plane"></i> 
              Отправить
            </button>
      </form>
    </div>
  </div>
</div>
</div>

<div class="row arrow-container">
  <a class="arrow-icon" href="#">
    <i class="fas fa-chevron-up fa-4x"></i>
  </a>
</div>

</section>
</template>

<script>
import data from "../../data/data.json";

export default {
  name: "Contact",
  props: {},
  components: {},
  data() {
    return {
      contact: data.contact,
      social: data.contact.social,
      heading: data.main.headings.contact,
      text: ""
    };
  },
  methods : {
        btnClick(event) {
            window.open(`${data.contact.formEndPoint}${encodeURIComponent(event)}`);
        }
    }
};
</script>

<style lang="scss"></style>
