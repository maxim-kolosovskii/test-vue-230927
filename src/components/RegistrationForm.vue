<template>
  <div class="page page_login">
    <div class="container">
      <h1 class="page__title">{{ title }}</h1>

      <p class="page__text">{{ msg }}</p>

      <p class="page__text" v-html="forRegistered"></p>

      <form class="form" @submit.prevent="onSubmit" action="https://vuejs.org/" method="post" novalidate>

        <!-- Функционал ошибки работает некорректно -->
        <div class="alert alert_warning" role="alert" v-if="errors.length">
          <h2>{{ errorMsg }}</h2>
          <ul>
            <li v-for="error in errors">{{ error }}</li>
          </ul>
        </div>

        <fieldset class="form__group">
          <input type="email" class="form__control" id="form-email" name="formEmail" placeholder="" v-model="email" required>
          <label for="form-email" class="form__label">{{ emailLabel }}*</label>
        </fieldset>

        <fieldset class="form__group">
          <input type="password" class="form__control" id="form-password" name="formPassword" placeholder="" v-model="password" required>
          <label for="form-password" class="form__label">{{ passwordLabel }}*</label>
        </fieldset>

        <fieldset class="form__group">
          <input type="password" class="form__control" id="form-password-confirm" name="formPasswordConfirm" placeholder="" v-model="passwordConfirmation" required>
          <label for="form-password-confirm" class="form__label">{{ passwordConfirmationLabel }}*</label>
        </fieldset>

        <fieldset class="form__group form__group_checkbox">
          <label for="form-checkbox" class="form__checkbox">
            <input type="checkbox" class="form-check-input" id="form-checkbox" v-model="checked">
          </label>
          <span class="form__checkbox-txt" v-html="checkboxMsg"></span>
        </fieldset>

        <fieldset class="form__group">
          <button type="submit" class="btn">{{ RegistrationButton }}</button>
        </fieldset>
      </form>
    </div>
  </div><!-- end page -->
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
        checked: false,
        checkboxMsg: 'Я принимаю <a href="#">Общие положения и условия</a> и <a href="#">Положение о безопасности данных</a>',
        requiredText: 'Это поле является обязательным',
        RegistrationButton: 'Зарегистрироваться',
        errors: [],
        errorMsg: 'Исправьте следующие ошибки:',
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
<style scoped lang="scss">
  @import '../assets/scss/_variables';

  %padding {
    padding: 1.03rem 1rem .55rem 9px;
  }

  %form__label_active {
    opacity: .25;
    padding-left: 14px;
    @include transform(translateY(1.15rem) scale(0.7));
  }

  .page_login {

    .container {
      @include box-sizing;
      @include margin-auto;
      @include transition(max-width $transition-duration $transition-timing-function);

      @media only screen and (max-width: 399px) {
        padding: 0 16px;
        width: 100%;
      }
      @media only screen and (max-width: 299px) {
        padding: 0 8px;
      }
      @media only screen and (min-width: 400px) {
        max-width: 290px;
      }
    }
  }

  .page__title {
    color: $color-green;
    @include title_3;
    margin: 2.5vh 0;
    text-align: center;
  }

  .page__text {
    color: $color-grey-dark;
    margin-bottom: 1.25vh;
    text-align: center;
  }


  /* Form elements */
  .form__group {
    border: 0;
    display: flex;
    @include reset;
    position: relative;
    top: auto; left: auto;

    &:not(.form__group_checkbox) {
      flex-direction: column-reverse;
    }
  }

  .form__control {
    background-color: #fff;
    border: 0 none;
    border-bottom: 1px solid $color-grey-medium;
    @include box-sizing;
    display: block;
    font-size: 1rem;
    outline: none;
    @extend %padding;
    width: 100%;
    transition: all 0.25s ease;

    &:hover,
    &:focus {
      border-bottom-color: $color-grey-dark;
      color: $color-black;
    }
    &:focus {
      outline: none;
    }

    &:focus, &:not(:placeholder-shown), &:-webkit-autofill {
      & + .form__label {
        @extend %form__label_active;
      }
    }
  }

  .form__label {
    cursor: text;
    opacity: .4;
    padding-left: 8px;
    pointer-events: none;
    transform-origin: left top;
    @include transform(translateY(2.3rem));
    @include transition(all $transition-duration-fast $transition-timing-function);
  }

  /* Checkbox */
  .form__group_checkbox {
    margin-bottom: 2vh;

    @include media-tablet-v-mx {
      padding: 4vh 0 2vh;
    }
    @include media-phablet-mx {
      padding-bottom: 4vh;
    }
    @include media-tablet-v-mn {
      padding: 4vh 0 2vh;
    }
  }

  label.form__checkbox {
    margin: -3px 0 3px;
  }

  input[type="checkbox"] {
    background-color: #fff;
    border: 1px solid $color-grey-medium;
    cursor: pointer;
    height: 30px;
    margin: 0 10px 0 1px;
    width: 30px;
    position: relative;
    @include x-appearance(none);
    transition: all $transition-duration-fast $transition-timing-function;

    &:checked {
      border: 1px solid #bcbcbc;

      &:after {
        content: '';
        position: absolute;
        left: 10px;
        top: 3px;
        width: 10px;
        height: 17px;
        border: solid $color-black;
        border-width: 0 2px 2px 0;
        @include transform(rotate(45deg));
      }
    }
  }

  .form__checkbox-txt {
    font-size: 0.8rem;
  }


  /* Button */
  %hover {
    background-color: $color-blue-dark;
    border: 1px solid $color-blue-dark;
    @include box-shadow(none);
    color: $color-orange;
    text-decoration: none;
  }

  .btn {
    @include b-radius(0);
    @include box-sizing;
    background-color: $color-blue;
    border: 1px solid $color-blue;
    color: #fff;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: $font-family-accent;
    font-weight: $font-weight-500;
    letter-spacing: 1px;
    line-height: 1.24; //24px
    outline: none;
    position: relative;
    text-align: center;
    @include transition(all $transition-duration-fast $transition-timing-function);

    @include media-tablet-h-mx {
      font-size: inherit; //16px
      min-height: 48px;
    }
    @include media-tablet-h-mn {
      font-size: 1.25rem;
      min-height: 58px;
    }

    &:focus {
      outline: 3px solid $color-blue-light;
    }

    &:hover {
      @extend %hover;
    }

    &.disabled,
    &:disabled {
      color: #94d0ff;
      pointer-events: none;
      @include user-select(none);
    }
  }


  /* Alert */
  .alert_warning {
    background-color: lighten($color-orange, 40%);
    color: darken($color-orange, 20%);
    padding: 3vh 1vw;

    h2 {
      @include title_6;
      font-weight: $font-weight-700;
      margin-bottom: 1vh;
    }

    ul {
      @include reset;
    }

    li {
      font-size: 0.8rem;
      line-height: 1.3;
      padding-bottom: 1vh;
      margin-left: 12px;
    }
  }
</style>
