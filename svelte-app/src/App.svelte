<script>
import {onMount} from "svelte"
	import { fade } from 'svelte/transition';
	import { elasticOut } from 'svelte/easing';

	let visible = false;

	function spin(node, { duration }) {
		return {
			duration,
			css: t => {
				const eased = elasticOut(t);

				return `
					transform: scale(${eased}) rotate(${eased * 1080}deg);
					color: hsl(
						${~~(t * 360)},
						${Math.min(100, 1000 - 1000 * t)}%,
						${Math.min(50, 500 - 500 * t)}%
					);`
			}
		};
	}

	onMount(() => {
		visible = true;
	})
</script>

<style>
	.centered {
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%,-50%);
	}

	.content {
		position: absolute;
		transform: translate(-50%,-50%);
		font-size: 4em;
		text-align: center;
	}

	.content img{
		max-height: 100px;
	}
</style>


{#if visible}
	<div class="centered" in:spin="{{duration: 8000}}" out:fade>
	<div class="content">
		<img src="foti_logo.png" alt="logo"/>
		<span>Frontenders Ticino</span>
		</div>
	</div>
{/if}