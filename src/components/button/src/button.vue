<template>
  <button
    class="cr-button"
    @click="handleClick"
    :disabled="buttonDisabled || loading"
    :autofocus="autofocus"
    :type="nativeType"
    :class="[
      type ? 'cr-button--' + type : '',
      buttonSize ? 'el-button--' + buttonSize : '',
      {
        'is-disabled': buttonDisabled,
        'is-loading': loading,
        'is-plain': plain,
        'is-round': round,
        'is-circle': circle
      }
    ]"
  >
    <i class="el-icon-loading" v-if="loading"></i>
    <i :class="icon" v-if="icon && !loading"></i>
    <span v-if="$slots.default"><slot></slot></span>
  </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component({
  name: 'CrButton',
  components: {}
})
export default class extends Vue {
  @Prop({ default: 'default' }) private type?: string
  @Prop({ default: 'button' }) private nativeType?: string
  @Prop({ default: '' }) private icon?: string
  @Prop(String) private size?: string
  @Prop(Boolean) private loading?: boolean
  @Prop(Boolean) private disabled?: boolean
  @Prop(Boolean) private plain?: boolean
  @Prop(Boolean) private autofocus?: boolean
  @Prop(Boolean) private round?: boolean
  @Prop(Boolean) private circle?: boolean

  get buttonSize() {
    return this.size
  }

  get buttonDisabled() {
    return this.disabled
  }

  private handleClick(evt: any) {
    this.$emit('click', evt);
  }
}
</script>