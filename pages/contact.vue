<template>
  <main>
    <div class="custom-container p-2">
      <h1 class="my-4 border-bottom d-inline-block">Contact Info</h1>
      <div class="stuff d-flex justify-content-around align-items-center">
        <iframe
          class="col-lg-6"
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d23462.31910890794!2d-76.85238457418735!3d41.01914629829463!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x89cf0d2f4cf23c55%3A0xb67e5d036e6477c1!2s704%20Klinetob%20Rd%2C%20Milton%2C%20PA%2017847!5e1!3m2!1sen!2sus!4v1567349677392!5m2!1sen!2sus"
          frameborder="0"
          style="border:0;"
          allowfullscreen
        ></iframe>
        <div class="col-lg-6 d-flex flex-column align-items-start">
          <div class="d-flex">
            <div>
              <h1>Contact</h1>
              <h3 class="mb-0">Joan Klinetob Harrison</h3>
              <div class="mt-2">
                Phone: <a href="tel:5714497136">(571) 449-7136</a> 
              </div>
              Email: <a class="mt-3" href="mailto:joanhar@gmail.com">joanhar@gmail.com</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import axios from 'axios'
export default {
  head() {
    return { title: 'Contact' }
  },
  data() {
    return {
      name: '',
      phone: '',
      email: '',
      message: '',
      btnText: 'Send'
    }
  },
  methods: {
    submitInquiry() {
      const { name, phone, email, message } = this
      this.btnText = 'Sending...'
      const postAddress = '/.netlify/functions/mailgun-form'
      axios
        .post(
          postAddress,
          {
            name,
            phone,
            email,
            message
          },
          { headers: { 'Content-Type': 'application/x-www-form-urlencoded' } }
        )
        .then(({ data }) => (this.btnText = 'Successfully Sent!'))
        .catch(
          ({ data }) =>
            (this.btnText =
              'Something broke.  Will punish the developer harshly for this.')
        )
    }
  }
}
</script>

<style scoped>
iframe {
  height: 600px;
}
img {
  max-height: 240px;
  border-radius: 5px;
  box-shadow: 5px 5px 5px 5px rgb(242, 255, 255);
}
@media screen and (max-width: 990px) {
  iframe {
    height: 400px;
  }
  .stuff {
    flex-wrap: wrap-reverse;
  }
}
</style>