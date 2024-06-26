<script lang="ts">
  import type { HTMLSelectAttributes } from 'svelte/elements';

  import { twMerge as merge } from 'tailwind-merge';

  import type { SelectOptionValue } from '$lib/types/global';

  import Option from './simple-option.svelte';

  interface $$Props extends HTMLSelectAttributes {
    id: string;
    value: SelectOptionValue;
    name?: string;
    options?: SelectOptionValue[];
    label?: string;
    labelHidden?: boolean;
    arrow?: boolean;
    'data-testid'?: string;
  }

  let className: string = null;
  export { className as class };
  export let id: string;
  export let value: SelectOptionValue;
  export let label: string = null;
  export let arrow = false;
  export let name = id;
  export let options: SelectOptionValue[] = [];
</script>

<div>
  <label class="sr-only" for={id}>{label}</label>
  <select
    class={merge(
      'inline h-10 w-full rounded-lg border px-2 text-base',
      className,
    )}
    class:remove={arrow}
    {name}
    {id}
    bind:value
    on:change
    {...$$restProps}
  >
    <slot>
      {#each options as option}
        <Option value={option} />
      {/each}
    </slot>
  </select>
</div>

<style lang="postcss">
  select {
    @apply border-secondary bg-transparent text-primary outline-none focus-visible:outline focus-visible:outline-blue-700;
  }

  .remove {
    @apply h-8 appearance-none rounded-xl py-1 pl-3 text-sm;
  }
</style>
