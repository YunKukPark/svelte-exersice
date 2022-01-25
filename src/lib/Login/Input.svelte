<script>
	export let name;
	export let value;
	export let placeholder;
	export let type;

	const handleInput = (e) => (value = e.target.value);
</script>

<input
	{name}
	{type}
	{placeholder}
	on:input={handleInput}
	class="w-full h-full px-4 py-2 pl-10 border border-solid border-border rounded-sm  focus:border focus:border-blue-primary focus:outline-none transition"
/>
