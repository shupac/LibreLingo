<script>
  import { createEventDispatcher } from "svelte"

  const dispatch = createEventDispatcher()
  export let href
  export let primary = false
  export let light = false
  export let info = false
  export let inverted = false
  export let outlined = false
  export let hidden = false
  export let color = null
  export let textColor = null
  export let customColor = color != null
  export let customTextColor = textColor != null
  export let target = "_self"
  export let size = "default"
  export let type = "button"
  export let tabindex = 0
  export let key = false
  export let disabled = false

  let styleTokens = `
    --color:${color};
    --textColor:${textColor};
  `
</script>

{#if href}
  <a
    style="{styleTokens}"
    class="button is-{size}"
    class:is-primary="{primary}"
    class:is-light="{light}"
    class:is-info="{info}"
    class:is-inverted="{inverted}"
    class:is-outlined="{outlined}"
    class:is-hidden="{hidden}"
    class:customColor
    class:customTextColor
    class:key
    {href}
    {tabindex}
    {target}>
    <slot />
  </a>
{:else}
  <button
    style="{styleTokens}"
    class="button is-{size}"
    class:is-primary="{primary}"
    class:is-light="{light}"
    class:is-info="{info}"
    class:is-inverted="{inverted}"
    class:is-outlined="{outlined}"
    class:is-hidden="{hidden}"
    class:customColor
    class:customTextColor
    class:key
    on:click="{() => dispatch('click')}"
    {tabindex}
    {disabled}
    {type}>
    <slot />
  </button>
{/if}

<style>
  .button.customColor {
    background-color: var(--color);
  }

  .button.customTextColor {
    color: var(--textColor);
  }

  .key {
    font-family: monospace;
    margin: 1em;
    margin-left: 0;
    margin-top: 0;
  }
</style>
