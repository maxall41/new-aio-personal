<script>
	export let id;
	let claps = 0
	import { API_URL } from "@/data/constants";
  import Button from "./Button.svelte"


	async function clap() {
		const clapRequest = await fetch(API_URL + "api/claps/increment", {
				method: "POST",
				body: JSON.stringify({
					post_title: id,
				}),
			});
			claps++;
	}

	async function fetch_clap_data() {
		let url = API_URL + "api/claps/get?post_title=" + id;
		const getClapsRequest = await fetch(url);
		const clapsResult = await getClapsRequest.json();
		if (clapsResult.claps != null) {
			claps = clapsResult.claps;
		}
	}

	fetch_clap_data()
</script>


<Button client:load on:click={clap}>
  <i class="fa-solid fa-hands-clapping light:text-black dark:text-textColor"></i><span class="ml-2" id="clap-count">{claps}</span
>
</Button>
