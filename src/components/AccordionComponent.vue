<template lang="pug">
  div(class="accordion-container")
    span(class="accordion-container__label") EXCLUSIVO HOTELES.COM
    button(class="accordion-container__btn" @click="accordionAction($event)") {{ title }}
    div(class="accordion-container__content")
      slot
</template>

<script>
export default {
  name: 'AccordionComponent',
  props: {
    title: {
      type: String,
      default: 'Insert Accordion Title'
    }
  },
  methods: {
    // Funcionalidad click acordeón
    accordionAction (e) {
      // Toggle sobre la clase 'active' en el botón
      e.target.classList.toggle('active')
      // Toggle sobre el panel con la clase 'show'
      e.target.nextSibling.classList.toggle('show')
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '~scss/application';

  .accordion-container {
    border: $accordion-border;
    position: relative;
    background: $accordion-container-bgcolor;
    margin: 0 10px;

    ~ .accordion-container {
      margin-top: 24px;
    }

    @include if-tablet-portrait {
      padding: 0 30px;
    }

    &__label {
      position: absolute;
      top: 0;
      right: 0;
      background: $accordion-label-bgcolor;
      font-family: $accordion-label-font-family;
      font-weight: 400;
      color: $accordion-label-color;
      font-size: 7px;
      letter-spacing: 1.52px;
      padding: 5px 20px;

      @include if-tablet-portrait {
        font-size: 12px;
      }
    }

    &__btn {
      background-color: $accordion-bgcolor;
      width: 100%;
      height: $accordion-height;
      font-family: $accordion-title-font-family;
      color: $accordion-title-color;
      font-size: 21px;
      font-weight: 700;
      line-height: 38px;
      cursor: pointer;
      border: none;
      text-align: left;
      outline: none;
      padding: 0 0 0 6px;

      @include if-tablet-portrait {
        font-size: 24px;
        padding: 0;
      }

      &::before {
        content: url('../assets/accordion-component/angle-down-blue.svg');
        margin-right: 6px;
        transition: all .2s linear;
        float: left;

        @include if-tablet-portrait {
          margin-right: 20px;
        }
      }

      &::after {
        content: 'Opcional';
        font-family: $accordion-title-optional-font-family;
        color: $accordion-title-optional-color;
        font-weight: 400;
        font-size: 12px;
        margin-left: 18px;
        transition: all .2s linear;
      }

      &.active::before {
        transform: rotate(-180deg) translateY(-7%);
      }
    }

    &__content {
      background-color: white;
      max-height: 0;
      overflow: hidden;
      transition: .5s ease-in-out;
      opacity: 0;

      &.show {
        opacity: 1;
        max-height: 100%;
      }
    }
  }
</style>
