<template>
<div>
   <form @submit.prevent="sendForm" name="contact" method="POST" data-netlify="true" netlify-honeypot="bot-field">
     <p class="hidden" style="display: none;">
        <label>Don't fill this out if you're human:
          <input name="bot-field"/>
        </label>
      </p>
      <p>
        <label>Your Name: <input v-model="form.name"     type="text" name="name" /></label>   
      </p>
      <p>
        <label>Your Email: <input v-model="form.email"      type="email" name="email" /></label>
      </p>
      <p>
        <label>Message: <textarea v-model="form.message"    name="message"></textarea></label>
      </p>
      <p>
        <button type="submit">Send</button>
      </p>
</form>
</div>
  
<!------
   netlify
   data-netlify="true"
   data-netlify-honeypot="bot-field"
   name属性
   formのmethod

-------->
</template>

<script>

export default {
   data() {
      return {
         form: {
            name: '',
            email: '',
            message: ''
         }
      }
   },
   methods: {
      encode(data) {
         return Object.keys(data)
         .map(key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`)
         .join('&')
      },
      sendForm() {
         fetch('/', {
            method: 'post',
            headers: {
               "Content-Type": "application/x-www-form-urlencoded"
            },
            body: this.encode({
               'form-name': 'contact',
               ...this.form
            })
         })
         .then(() => this.$router.push('/success'))
         .catch(() => this.$router.push('/fail'))
      }
   }
}
</script>

<style scoped>

</style>