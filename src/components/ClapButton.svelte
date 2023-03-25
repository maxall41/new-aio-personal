<script>
	export let id;
	let claps = 0
	import { API_URL } from "@/data/constants";

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


<button
	class="group relative h-9 w-16 rounded-md bg-zinc-200 p-2 ring-zinc-400 transition-all hover:ring-2 dark:bg-zinc-700"
	on:click={clap}
	><i class="fa-solid fa-hands-clapping text-white"></i><span class="ml-2" id="clap-count">{claps}</span
	></button
>
