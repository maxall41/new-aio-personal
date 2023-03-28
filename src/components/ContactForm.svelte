<script>
  import { form, field } from 'svelte-forms';
  import { required, email } from 'svelte-forms/validators';

  const emailField = field('email', '', [required(),email()]);
  const messageField = field('message', '', [required()]);
  const contactForm = form(emailField,messageField);

  async function submit() {
    const contactRequest = await fetch(API_URL + "api/contact/submit", {
				method: "POST",
				body: JSON.stringify({
					email: emailField.value,
          message: messageField.value
				}),
			});
      console.log(contactRequest)
  }
</script>


<section>
  <div class="mb-4">
      <label class="block text-textColor  text-sm font-bold mb-2" for="email">
        Email:
      </label>
      <input class="input-primary " id="email" type="text" placeholder="max@hello.world"  bind:value={$emailField.value} />
    </div>
    <div class="mb-4">
      <label class="block text-textColor  text-sm font-bold mb-2" for="message" >
        Message:
      </label>
     <input class="input-primary pb-32 text-start" id="message" type="text" placeholder="Hello, World!"  bind:value={$messageField.value} />
    </div>

<script src="https://challenges.cloudflare.com/turnstile/v0/api.js" async defer></script>
  <button on:click={submit} class="relative h-9 w-full rounded-md bg-zinc-200 p-2 ring-zinc-400 transition-all hover:ring-2 dark:bg-zinc-700" disabled={!$contactForm.valid}>Submit</button>
</section>