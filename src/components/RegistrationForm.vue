<template>
  <div class="container" style="max-width: 290px;">
    <div class="row">
      <div class="col">

        <h1 class="page-title">{{ title }}</h1>

        <p class="form-text">{{ msg }}</p>

        <p class="page-info form-text" v-html="forRegistered"></p>

        <form @submit.prevent="onSubmit" action="https://vuejs.org/" method="post" novalidate>

          <div class="form-text alert alert-warning" role="alert" v-if="errors.length">
            <p><strong>{{ errorMsg }}</strong></p>
            <ul class="mb-0">
              <li v-for="error in errors">{{ error }}</li>
            </ul>
          </div>

          <fieldset class="form-group">
            <label for="form-email">{{ emailLabel }}*</label>
            <input type="email" class="form-control" id="form-email" name="formEmail" v-model="email" required>
          </fieldset>

          <fieldset class="form-group">
            <label for="form-password">{{ passwordLabel }}*</label>
            <input type="password" class="form-control" id="form-password" name="formPassword" v-model="password" required>
          </fieldset>

          <fieldset class="form-group">
            <label for="form-password-confirm">{{ passwordConfirmationLabel }}*</label>
            <input type="password" class="form-control" id="form-password-confirm" name="formPasswordConfirm" v-model="passwordConfirmation" required>
          </fieldset>

          <fieldset class="form-group form-check">
            <input type="checkbox" class="form-check-input" id="form-checkbox" v-model="checked">
            <label for="form-checkbox" class="form-check-label form-text" v-html="checkboxMsg"></label>
          </fieldset>

          <fieldset class="form-group">
            <button type="submit" class="btn btn-primary">{{ RegistrationButton }}</button>
          </fieldset>
        </form>

      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'FormRegistration',
    data () {
      return {
        title: 'Регистрация',
        msg: 'Пожалуйста, заполните эту форму, чтобы создать учетную запись.',
        forRegistered: 'Уже зарегистрированы? <br><a href="#">Войти в Личный кабинет</a>',
        emailLabel: 'Адрес электронной почты',
        email: '',
        passwordLabel: 'Пароль',
        password: '',
        passwordConfirmationLabel: 'Повторите пароль',
        passwordConfirmation: '',
        checked: [],
        checkboxMsg: 'Я принимаю <a href="#">Общие положения и условия</a> и <a href="#">Положение о безопасности данных</a>',
        requiredText: 'Это поле является обязательным',
        RegistrationButton: 'Зарегестрироваться',
        errorMsg: 'Исправьте следующие ошибки:',
        errors: [],
        formEmail: null,
        formPassword: null,
        formPasswordConfirm: null
      }
    },
    methods: {
      onSubmit: function (e) {
        if (this.formEmail && this.formPassword && this.formPasswordConfirm) {
          return true;
        }

        this.errors = [];

        if (!this.formEmail) {
          this.errors.push('Заполните адрес электронной почты.');
        }
        if (!this.formPassword) {
          this.errors.push('Введите пароль.');
        }
        if (!this.formPasswordConfirm) {
          this.errors.push('Введите пароль повторно.');
        }

        e.preventDefault();

        console.log("onSubmit", this.email, this.password)
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .page-title {
    color: #3b7aa5;
  }

  .page-title,
  .page-info,
  .form-group,
  .alert-warning {
    margin-bottom: 3vh;
  }

  .form-group:not(:last-child) {
    text-align: left;
  }

  .alert-warning {
    padding-left: 18px;
    text-align: left;
  }

  .alert-warning li {
    line-height: 1.3;
    padding-bottom: 1vh;
  }
</style>
