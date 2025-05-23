<script>
	import { onMount, getContext } from 'svelte';
	import { createEventDispatcher } from 'svelte';
	
	// Event dispatcher to communicate with parent component
	const dispatch = createEventDispatcher();
	const i18n = getContext('i18n'); 

	// Role data structure
	const roles = [
		{
			id: 'user',
			title: 'Student',
			icon: '👨‍🎓',
			features: [
				'Personalized learning path',
				'Track your progress',
				'Access study materials',
				'Connect with tutors'
			],
			buttonColor: 'bg-blue-500 hover:bg-blue-600',
			iconBgColor: 'bg-blue-100'
		},
		{
			id: 'teacher',
			title: 'Teacher',
			icon: '👨‍🏫',
			features: [
				'Manage your classes',
				'Monitor student progress',
				'Create assignments',
				'AI teaching assistant'
			],
			buttonColor: 'bg-green-500 hover:bg-green-600',
			iconBgColor: 'bg-green-100'
		},
		{
			id: 'parent',
			title: 'Parent',
			icon: '👨‍👧',
			features: [
				"Track child's progress",
				'Communication with teachers',
				'View performance reports',
				'Schedule consultations'
			],
			buttonColor: 'bg-purple-500 hover:bg-purple-600',
			iconBgColor: 'bg-purple-100'
		}
	];

	// Function to handle role selection
	function selectRole(roleId) {
		console.log(`Selected role: ${roleId}`);
		// Dispatch event to parent component
		dispatch('roleSelected', { role: roleId });
	}

	onMount(() => {
		// Add any initialization code here if needed
		console.log('Role selection page mounted');
	});
</script>

<div class="min-h-screen bg-[#F0F9FF] border border-blue-200 flex flex-col justify-center items-center p-4 overflow-auto">

	<main class="w-full max-w-6xl mx-auto pt-16">
		<div class="text-center mb-8">
			<h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-2">{$i18n.t('Choose Your Role')}</h1>
			<p class="text-gray-600">{$i18n.t('Select the role that best describes you')}</p>
		</div>

		<!-- Role cards container -->
		<div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
			{#each roles as role, i}
				<div class="bg-white rounded-lg shadow-md p-6 flex flex-col items-center border transition-transform">
					<div
						class="w-16 h-16 rounded-full {role.iconBgColor} flex items-center justify-center mb-4 text-3xl"
					>
						{role.icon}
					</div>

					<h2 class="text-xl font-bold mb-4 text-gray-900">{$i18n.t(role.title)}</h2>

					<ul class="w-full space-y-2 mb-6">
						{#each role.features as feature}
							<li class="flex items-start">
								<span class="text-green-500 mr-2">✓</span>
								<span class="text-gray-700">{$i18n.t(feature)}</span>
							</li>
						{/each}
					</ul>

					<button
						on:click={() => selectRole(role.id)}
						class="{role.buttonColor} w-full py-2 rounded-md text-white font-medium transition-colors duration-300"
					>
						{$i18n.t('Select Role')}
					</button>
				</div>
			{/each}
		</div>

		<!-- Note -->
		<div class="text-center max-w-xl mx-auto">
			<p class="text-sm text-gray-600">
				{$i18n.t('Note: Your role determines the features and access levels available to you. You can request a role change later if needed.')}
			</p>
		</div>
	</main>
</div>