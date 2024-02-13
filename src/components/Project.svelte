<script>
    import { API_URL } from "@/data/constants";

    export let title;
    export let description;
    export let url;
    export let disable_stars;

    let stars = -1
    async function fetch_star_data() {
		let call_url = API_URL + "api/github/get-star-count?project_url=" + url;
		const getClapsRequest = await fetch(call_url);
		const stars_result = await getClapsRequest.json();
		console.log(stars_result)
		if (stars_result.result != null) {
			stars = stars_result.result;
			console.log("Set stars to " + stars)
		}
	}

	if (url != null && disable_stars != true) {
	 fetch_star_data()
	}
</script>

<li class="mt-4">
	<a
		href={url}
		target="_blank"
		rel="noopener noreferrer"
		class="cactus-link inline-block"
	>{title}
	</a>:
	<p class="mt-2">Github Star(s): {stars != -1 ? stars : "N/A"}️</p>
	<p class="inline-block sm:mt-2">
		{description}
	</p>
</li>
