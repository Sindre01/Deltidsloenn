<script>
	 import Select, { Option } from '@smui/select';
	import Icon from '@smui/select/icon';
	
	let fruits = ['Apple', 'Orange', 'Banana', 'Mango'];
	
	let value = '';
	let valueHelperText = '';
	let valueLeadingIcon = '';
	let valueInvalid = '';
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		UB-Kalkulator
	</h1>

	<h2>
		Regner ut lønn inkludert kveldstillegg
	</h2>

	<div>
		<Select
		  class="shaped-outlined"
		  variant="outlined"
		  bind:value={valueLeadingIcon}
		  label="Leading Icon"
		>
		  <Icon class="material-icons" slot="leadingIcon">event</Icon>
		  <Option value="" />
		  {#each fruits as fruit}
			<Option value={fruit}>{fruit}</Option>
		  {/each}
		</Select>
	 
		<pre class="status">Selected: {valueLeadingIcon}</pre>
	  </div>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	h1 {
		width: 100%;
		font-style: italic;
	}

	* :global(.shaped-outlined),
  * :global(.shaped-outlined .mdc-select__anchor) {
    border-radius: 28px;
  }
  * :global(.shaped-outlined .mdc-text-field__input) {
    padding-left: 32px;
    padding-right: 0;
  }
  *
    :global(.shaped-outlined
      .mdc-notched-outline
      .mdc-notched-outline__leading) {
    border-radius: 28px 0 0 28px;
    width: 28px;
  }
  *
    :global(.shaped-outlined
      .mdc-notched-outline
      .mdc-notched-outline__trailing) {
    border-radius: 0 28px 28px 0;
  }
  * :global(.shaped-outlined .mdc-notched-outline .mdc-notched-outline__notch) {
    max-width: calc(100% - 28px * 2);
  }
  *
    :global(.shaped-outlined.mdc-select--with-leading-icon
      .mdc-notched-outline:not(.mdc-notched-outline--notched)
      .mdc-floating-label) {
    left: 16px;
  }
</style>
