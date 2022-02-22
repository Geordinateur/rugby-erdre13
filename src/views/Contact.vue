<template>
  <div class="about">
    <h1>Contactez moi</h1>
    <form class="form" method="post" @submit="sendMail">
      <div>
        <label class="form label" for="email"></label>
        <input class="form input" v-model="form.from" type="email" name="email" id="email" placeholder="Votre adresse mail" required>
      </div>
      <div>
        <label class="form label" for="object"></label>
        <input class="form input" v-model="form.subject" type="text" name="subject" id="subject" placeholder="L'objet" required>
      </div>
      <div>
        <label class="form label" for="message"></label>
        <textarea class="form textarea" v-model="form.text" name="message" id="message"></textarea>
      </div>
      <div>
        <button class="form button" type="submit">Envoyer le message</button>
      </div>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  components: {
  },
  data()  {
    return {
      form: {
        from: '',
        subject: '',
        text: '',
      }
    }
  },
  // définition des méthodes d'objet
  methods: {
    sendMail: function (event) {
      event.preventDefault()
      axios
        .post('/mail', this.form)
        .then((response) => {
          console.log(response.data.message)
          this.$emit('alert', { messageAlert: JSON.parse(response.request.response).message, statusAlert: 'success', showAlert: true})
          this.form.from = ""
          this.form.subject = ""
          this.form.text = ""
        })
        .catch((error) => {
          console.log(error.response.data.message)
          this.$emit('alert', { messageAlert: JSON.parse(error.request.response).message, statusAlert: 'error', showAlert: true})
        });
    },
  }

}
</script>