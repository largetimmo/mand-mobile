<template>
  <div class="md-example-child md-example-child-stepper md-example-child-stepper-3">
    <md-field>
      <md-field-item
        name="arrow4"
        title="步进2, 只允许输入整数"
        customized
        align="right">
        <div class="normal-tip">
          <md-stepper
            v-model="value"
            :step="2"
            :min="2"
            is-integer
          ></md-stepper>
        </div>
      </md-field-item>
    </md-field>
  </div>
</template>

<script>import {Stepper, Field, FieldItem} from 'mand-mobile'

export default {
  name: 'stepper-demo',
  /* DELETE */
  title: '步进2',
  titleEnUS: 'Step 2',
  codeSandBox: 'https://codesandbox.io/s/vy5xymyvv0',
  /* DELETE */
  components: {
    [Field.name]: Field,
    [FieldItem.name]: FieldItem,
    [Stepper.name]: Stepper,
  },
  data() {
    return {
      value: 3,
    }
  },
}
</script>