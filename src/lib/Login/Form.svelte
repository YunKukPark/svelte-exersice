<script>
	import FaRegUserCircle from 'svelte-icons/fa/FaRegUserCircle.svelte';
	import FaLock from 'svelte-icons/fa/FaLock.svelte';
	import FaRegEyeSlash from 'svelte-icons/fa/FaRegEyeSlash.svelte';
	import FaRegEye from 'svelte-icons/fa/FaRegEye.svelte';

	const userInfo = { id: '', password: '' };

	let isPasswordView = false;
	let passwordViewType = 'password';
	const togglePasswordView = () => {
		isPasswordView = !isPasswordView;
		isPasswordView ? (passwordViewType = 'text') : (passwordViewType = 'password');
	};

	const onSubmit = (e) => {
		if (!userInfo.id || !userInfo.password) return alert('유저 정보를 입력해주세요');
		const loginSubmitForm = { method: 'POST', body: { ...userInfo } };
		console.log('api.loginEndpoint', { ...loginSubmitForm });
		alert('console 창에서 submitForm을 확인할 수 있습니다.');
	};
</script>

<div>
	<h2
		class="relative text-center text-blue-primary p-4 mb-5 after:content-[''] after:absolute after:bottom-1 after:left-1/2 after:-translate-x-1/2 after:w-24 after:h-0.5 after:bg-blue-primary"
	>
		Account Login
	</h2>
	<form on:submit|preventDefault={onSubmit}>
		<div class="input-wrapper relative items-center  mb-3">
			<div
				class="absolute left-3 top-1/2 -translate-y-1/2 text-blue-primary w-5 h-5 mr-2 flex items-center justify-center "
			>
				<FaRegUserCircle />
			</div>
			<input
				name="id"
				type="text"
				bind:value={userInfo.id}
				placeholder="Username: admin or user"
				class="w-full h-full px-4 py-2 pl-10 border border-solid border-border rounded-sm  focus:border focus:border-blue-primary focus:outline-none transition"
			/>
		</div>

		<div class="input-wrapper relative items-center  mb-5">
			<div
				class="absolute left-3 top-1/2 -translate-y-1/2 text-blue-primary w-5 h-5 mr-2 flex items-center justify-center "
			>
				<FaLock />
			</div>
			<!-- 2way binding issue -->
			<input
				bind:value={userInfo.password}
				name="password"
				type="password"
				{passwordViewType}
				placeholder="Password 를 입력해주세요"
				class="w-full h-full px-4 py-2 px-10 border border-solid border-border rounded-sm  focus:border focus:border-blue-primary focus:outline-none transition"
			/>
			<div
				on:click={togglePasswordView}
				class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 w-5 h-5 mr-2 flex items-center justify-center cursor-pointer"
			>
				{#if isPasswordView}
					<FaRegEye />
				{:else}
					<FaRegEyeSlash />
				{/if}
			</div>
		</div>

		<div class="flex justify-between items-center mb-5">
			<div>
				<input name="user-login-remember" type="checkbox" />
				<label htmlFor="user-login-remember">Remember Me</label>
			</div>
			<a href="#" class="text-blue-primary">Forgot Password?</a>
		</div>

		<button
			class="w-full text-center py-2 bg-blue-primary text-white rounded-sm hover:bg-blue-500 transition"
			>Submit</button
		>
	</form>
</div>
