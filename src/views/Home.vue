<template>
  <div class="page-wrapper">
    <div class="content-section">
      <h1 class="page-title">Learn to code by watching others</h1>
      <p class="page-content">
        See how experienced developers solve problems in real-time. Watching
        scripted tutorials is great, but understanding how developers think is
        invaluable.
      </p>
    </div>

    <div class="form-section">
      <p class="incentive-text">Try it free 7 days then $20/mo. thereafter</p>

      <form class="signup-form" action="#" method="POST">
        <div class="input-wrapper">
          <div
            :class="{ 'is-error': invalidForm.firstname }"
            class="input-field"
          >
            <input
              v-model="firstname"
              :class="{ 'is-error': invalidForm.firstname }"
              type="text"
              value=""
              name="firstname"
              placeholder="First Name"
            />
          </div>

          <p v-if="invalidForm.firstname" class="error-message">
            First Name cannot be empty
          </p>
        </div>

        <div class="input-wrapper">
          <div
            :class="{ 'is-error': invalidForm.lastname }"
            class="input-field"
          >
            <input
              v-model="lastname"
              :class="{ 'is-error': invalidForm.lastname }"
              type="text"
              value=""
              name="lastname"
              placeholder="Last Name"
            />
          </div>
          <p v-if="invalidForm.lastname" class="error-message">
            Last Name cannot be empty
          </p>
        </div>

        <div class="input-wrapper">
          <div
            :class="{ 'is-error': invalidForm.email }"
            class="input-field"
          >
            <input
              v-model="email"
              :class="{ 'is-error': invalidForm.email }"
              type="email"
              value=""
              name="email"
              placeholder="Email"
            />
          </div>
          <p v-if="invalidForm.email === 2" class="error-message">
            Email cannot be empty
          </p>
          <p v-else-if="invalidForm.email" class="error-message">
            Looks like this is not an email
          </p>
        </div>

        <div class="input-wrapper">
          <div
            :class="{ 'is-error': invalidForm.password }"
            class="input-field"
          >
            <input
              v-model="password"
              :class="{ 'is-error': invalidForm.password }"
              type="password"
              value=""
              name="password"
              placeholder="Password"
            />
          </div>
          <p v-if="invalidForm.password" class="error-message">
            Password cannot be empty
          </p>
        </div>

        <button type="submit" @click="validateForm">
          Claim your free trial
        </button>

        <p>
          By clicking the button, you are agreeing to our
          <a href="#">Terms and Services</a>
        </p>
      </form>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data() {
    return {
      firstname: '',
      lastname: '',
      email: '',
      password: '',
      invalidForm: {
        firstname: false,
        lastname: false,
        email: false,
        password: false
      }
    }
  },
  head() {
    return {
      title: {
        inner: 'Home'
      },
      meta: [
        {
          name: 'description',
          content: `${this.appTitle} home page`,
          id: 'desc'
        }
      ]
    }
  },
  methods: {
    validateForm(e) {
      e.preventDefault()

      const emailRegex = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      const emailState = emailRegex.test(String(this.email).toLowerCase())

      this.invalidForm.email = this.email.trim() === '' ? 2 : !emailState
      this.invalidForm.firstname = this.firstname.trim() === ''
      this.invalidForm.lastname = this.lastname.trim() === ''
      this.invalidForm.password = this.password.trim() === ''

      console.log(this.invalidForm)
    }
  },
  computed: mapState('app', ['appTitle'])
}
</script>

<style lang="scss" scoped>
@import '@/theme/variables.scss';

.page-wrapper {
  position: relative;
  padding: 7% 10%;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1;

  @media (max-width: 768px) {
    padding: 40px 24px;
    flex-direction: column;
  }
}

.content-section {
  width: 100%;
  max-width: 525px;
  margin-right: 45px;
  color: $light;

  @media (max-width: 768px) {
    margin-right: 0;
    margin-bottom: 64px;
    text-align: center;
  }

  .page-title {
    font-weight: bold;
    font-size: 50px;
    line-height: 55px;
    margin-bottom: 20px;

    @media (max-width: 1000px) {
      font-size: 36px;
      line-height: 44px;
    }

    @media (max-width: 768px) {
      font-size: 28px;
      line-height: 36px;
      text-align: center;
      letter-spacing: -0.291667px;
    }
  }

  .page-content {
    font-weight: 500;
    font-size: 16px;
    line-height: 26px;
  }
}

.form-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  max-width: 540px;

  .incentive-text {
    display: inline-block;
    width: 100%;
    padding: 17px 66px;
    margin-bottom: 24px;
    font-weight: bold;
    font-size: 15px;
    line-height: 26px;
    text-align: center;
    letter-spacing: 0.267857px;
    color: $light;
    background: $secondaryColor;
    box-shadow: 0 8px 0 rgba(0, 0, 0, 0.14688);
    border-radius: 10px;
  }

  .signup-form {
    display: flex;
    flex-direction: column;
    width: 100%;
    padding: 40px;
    background: $light;
    box-shadow: 0 8px 0 rgba(0, 0, 0, 0.14688);
    border-radius: 10px;

    @media (max-width: 768px) {
      padding: 24px;
    }

    .input-wrapper {
      display: flex;
      flex-direction: column;
      margin-bottom: 20px;

      @media (max-width: 768px) {
        margin-bottom: 16px;
      }

      p {
        margin-top: 5px;
        font-style: italic;
        font-weight: 500;
        font-size: 11px;
        line-height: 16px;
        text-align: right;
        color: $primaryColor1;
      }
    }

    .input-field{
      position:relative;

      &:after {
        content: '';
        position: absolute;
        top: 0;
        bottom: 0;
        right: 16px;
        display: block;
        margin: auto;
        height: 24px;
        width: 24px;
        background: url('../assets/img/error.svg') center no-repeat;
        background-size: cover;
        transition: opacity.3s ease-in-out;
        opacity: 0;
      }

      &.is-error:after {
        opacity: 1;
      }

    }

    input {
      position: relative;
      width: 100%;
      padding: 15px 32px;
      border: 1px solid $secondaryColor;
      box-sizing: border-box;
      border-radius: 5px;
      font-weight: 600;
      font-size: 14px;
      line-height: 26px;
      letter-spacing: 0.25px;
      color: $neutralColor1;
      outline: none;

      &::placeholder {
        mix-blend-mode: normal;
        opacity: 0.75;
      }

      &.is-error {
        border-color: $primaryColor1;
        color: $primaryColor1;

        &::placeholder {
          color: $primaryColor1;
        }
      }
    }

    button {
      margin-bottom: 23px;
      padding: 15px 0;
      background: $primaryColor2;
      box-shadow: inset 0px -4px 0px rgba(0, 0, 0, 0.0908818);
      border: none;
      border-radius: 5px;
      font-weight: 600;
      font-size: 15px;
      line-height: 26px;
      letter-spacing: 1px;
      text-transform: uppercase;
      color: $light;
      cursor: pointer;
      transition: background 0.3s ease-in-out;

      @media (max-width: 768px) {
        margin-bottom: 8px;
      }

      &:hover {
        background: lighten($primaryColor2, 15%);
      }
    }

    p {
      font-weight: 500;
      font-size: 11px;
      line-height: 26px;
      text-align: center;
      color: $neutralColor2;

      a {
        font-weight: bold;
        color: $primaryColor1;
      }
    }
  }
}
</style>
