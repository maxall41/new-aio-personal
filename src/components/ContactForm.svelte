<script>
  import { required, email } from 'svelte-forms/validators';
   import { Turnstile } from 'svelte-turnstile';
  import { API_URL } from '@/data/constants';
  import { form, field } from 'svelte-forms';

  const emailField = field('email', '', [required(),email()]);
  const messageField = field('message', '', [required()]);
  const contactForm = form(emailField,messageField);

  let token = ""

  function turnstileComplete(data) {
    console.log("CALL")
    console.log(data)
    token = data.token;
  }

  async function contactSubmit() {
    console.log("123");
    console.log(token)
    const contactRequest = await fetch(API_URL + "api/contact/submit", {
				method: "POST",
				body: JSON.stringify({
					email: emailField.value,
          message: messageField.value,
          turnstile_token: token
				}),
			});
      console.log(contactRequest);
  }

</script>

  <section  class="mb-4">
         <script src="https://challenges.cloudflare.com/turnstile/v0/api.js" async defer></script>
    <div class="mb-4 mt-4">
      <label class="block text-textColor  text-sm font-bold mb-2" for="email">
        Email:
      </label>
      <input class="input-primary " id="email" type="text" placeholder="max@hello.world"  bind:value={$emailField.value} />
    </div>
    <div class="mb-4">
      <label class="block text-textColor  text-sm font-bold mb-2" for="message" >
        Message:
      </label>
     <input class="input-primary pb-32 text-start mb-4" id="message" type="text" placeholder="Hello, World!"  bind:value={$messageField.value} />
     <Turnstile turnstile-callback={turnstileComplete} siteKey="0x4AAAAAAADj_D0FYcG1g4BO" />
    <button on:click={contactSubmit} class="relative h-9 w-full rounded-md bg-zinc-200 p-2 ring-zinc-400 transition-all hover:ring-2 mt-6 dark:bg-zinc-700" >Submit</button>
    </section>