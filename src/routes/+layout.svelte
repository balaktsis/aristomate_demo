<script lang='ts'>
	import { setupIonicBase } from 'ionic-svelte';

	/* Call Ionic's setup routine. */
	setupIonicBase();

	/* Import all components. (You can selectively import components instead; see below.) */
	import 'ionic-svelte/components/all';

	/* Theme variables */
	import '../theme/variables.css';

</script>

<ion-app>
	<slot />
</ion-app>