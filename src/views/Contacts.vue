<template>
  <div class="contacts">
    <div class="contacts__title">
      <h3>Let's work</h3>
      <span>Together</span>
    </div>
    <div class="contacts__content">
      <form
        action="#"
        class="contacts__form"
        id="feedbackForm"
        ref="feedbackForm"
      >
        <div class="contacts__field">
          <input
            type="text"
            name="email"
            v-model="form.email"
            class="contacts__input"
            placeholder="Email"
            required
            @input="errors.email = false"
          />
          <span v-if="errors.email" class="contacts__error">{{
            errors.email
          }}</span>
        </div>

        <div class="contacts__field">
          <input
            type="text"
            name="name"
            v-model="form.name"
            class="contacts__input"
            placeholder="Name"
            required
            @input="errors.name = false"
          />
          <span v-if="errors.name" class="contacts__error">{{
            errors.name
          }}</span>
        </div>

        <div class="contacts__field">
          <input
            type="text"
            name="message"
            v-model="form.message"
            class="contacts__input"
            placeholder="Message"
            required
            @input="errors.message = false"
          />
          <span v-if="errors.message" class="contacts__error">{{
            errors.message
          }}</span>
        </div>
        <button class="button" type="submit" @click.prevent="sendForm">
          Send
        </button>
      </form>
      <div class="contacts__feedback">
          <Transition>
            <img v-if="isSended" src="../assets/images/contacts.png" alt="" />
          </Transition>
          <Transition>
            <img  v-if="isLoading" class="contacts__loading" src="../assets/images/loading.gif" alt="">
          </Transition>
        <div class="contacts__info">
          <div class="contacts__social">
            <h5>Email</h5>
            <a target="_blank" href="mailto:andreevdaniil781@gmail.com">andreevdaniil781@gmail.com</a>
          </div>
          <div class="contacts__social">
            <h5>Telegram</h5>
            <a target="_blank" href="https://t.me/nfewft">@nfewft</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import emailjs from "emailjs-com";
export default {
  data() {
    return {
      form: {
        email: "",
        name: "",
        message: "",
      },
      isLoading: false,
      isSended: false,
      errors: {
        email: false,
        name: false,
        message: false,
      },
    };
  },
  methods: {
    sendForm() {
      this.errors = {email: false, name: false, message: false}
      if (!/^\w+@[a-zA-Z_]+?\.[a-zA-Z]{2,3}$/.test(this.form.email)) {
        this.errors.email = "You entered an invalid email.";
      }
      if (!/[a-zA-Z]/.test(this.form.name)) {
        this.errors.name = "You entered an invalid name.";
      }
      if (this.form.message.length < 5) {
        this.errors.message =
          "Please enter a message at least 5 characters long.";
      }
      if (this.errors.email || this.errors.name || this.errors.message) {
        return;
      }
      try {
        this.isLoading = true
        emailjs
          .sendForm(
            "service_6lqke3n",
            "template_hq16h5b",
            this.$refs.feedbackForm,
            "vLiaXOHyK7Wiwem4x",
            {
              name: this.form.name,
              email: this.form.email,
              message: this.form.message,
            }
          )
          .then(() => {
            this.isLoading = false;
            this.isSended = true;
            this.form = {name: '', email: '', message: ''}
          });
      } catch (error) {
        this.isLoading = false
      }
      // Reset form field
      this.name = "";
      this.email = "";
      this.message = "";
    },
  },
};
</script>
<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>