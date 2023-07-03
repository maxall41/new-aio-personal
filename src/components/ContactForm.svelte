<script>
  import Button from "./Button.svelte";
  import {SvelteToast, toast} from "@zerodevx/svelte-toast";
  const handleSubmit = async data => {
    toast.push("Sending...")
    const formData = new FormData(data.currentTarget)
    const object = Object.fromEntries(formData);
    const json = JSON.stringify(object);

    const response = await fetch("https://api.web3forms.com/submit", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
      },
      body: json
    });
    const result = await response.json();
    if (result.success) {
      toast.push("Message Sent!")
    }
  }
</script>
<SvelteToast />
<form on:submit|preventDefault={handleSubmit} class="flex flex-col" method="POST">

  <input type="hidden" name="access_key" value="b135ec5e-de25-4aa3-b5c8-e9eb70ef8f2b">
  <label for="name" class="mt-4 mb-2">Name:</label>
  <input id="name" type="text" name="name" class="p-1" required>
  <label for="email" class="mt-4 mb-2">Email:</label>
  <input  id="email" type="email" name="email" class="p-1" required>
  <label for="message" class="mt-4 mb-2">Message:</label>
  <textarea id="message" name="message" class="p-2" required></textarea>
  <div class="h-captcha mt-6 mb-6" data-captcha="true"></div>
  <Button class="w-full" type="submit">Send</Button>

</form>
