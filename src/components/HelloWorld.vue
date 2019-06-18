a
<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container">
        <a class="navbar-brand" href="#">Systeem Status</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
                aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
      </div>
    </nav>
    <div class="col-md-4 text-center">
      <h1 class="
        43font-weight-light">Services:</h1>
      <p class="lead">Hieronder is een lijst te vinden met services en hun status.</p>
    </div>
    <div class="row">
      <div class="col-md-4">


        <!--<ul class="list-group">-->
        <!--<li v-for="service in services" variant="success" class="list-group-item" v-on:click="clickedStatus(service)">Dapibus ac facilisis in</li>-->
        <!--</ul>-->
        <b-list-group>
          <div v-for="service in services">

            <b-list-group-item v-if="service.returncode >= 200 && service.returncode <= 300" v-on:click="clickedStatus(service)" variant="success">Service: {{service.serviceName}}<br> Up: {{service.isup}}</b-list-group-item>
            <b-list-group-item v-else v-on:click="clickedStatus(service)" variant="danger">Service: {{service.serviceName}}<br> Up: {{service.isup}}</b-list-group-item>

          </div>
        </b-list-group>
      </div>
      <div class="col-md-4" v-if="clicked !== null">
        <div class="row">
          <div class="col-md-4">
            <h4>Host online:</h4>
            <h4>Return code:</h4>
            <h4>Service name:</h4>
            <h4>Logs from body:</h4>

            <form :action="clicked.link">
              <button type="submit" class="btn btn-outline-secondary">Go to system</button>
            </form>
          </div>
          <div class="col-md-4">
            <h4>{{clicked.isup}}</h4>
            <h4>{{clicked.returncode}}</h4>
            <h4>{{clicked.serviceName}}</h4>
            <p>{{clicked.log}}</p>


          </div>

        </div>

      </div>
    </div>

  </div>
</template>
<script>
  import 'bootstrap/dist/css/bootstrap.css'
  import axios from 'axios';

  const qs = require('qs');
  export default {
    name: 'app',
    components: {},
    data() {
      return {
        services: [],
        clicked: null,
      }
    },

    mounted() {
      axios.get(`http://localhost:8080/status/api/check/`)
        .then(response => {
          this.services = response.data;
        })
        .catch(function (error) {
          alert("Somethings went wrong");
        })


    },
    methods: {
      clickedStatus: function (service) {
        this.clicked = service;
      },
      gotoLink: function () {

      }
    }
  }
</script>
