<script>
  import { page } from '$app/stores';  // Import page store
  import { goto } from '$app/navigation'; // Import goto for navigation

  let email = '';

  // Extract email from the URL query parameters
  $: email = $page.url.searchParams.get('email');

  function handleDismiss() {
    goto('/');  // Redirect back to the main page
  }
</script>

<main class="w-screen h-screen flex items-center justify-center text-[#222640] overflow-hidden">
  <div class="card variant-filled p-8 w-96 h-max flex flex-col items-center">
    <div>
      <span class="badge">
        <enhanced:img
          src="$lib/assets/icon-success.svg"
          alt=""
          class="suc-img w-12 h-12"
        />
      </span>
      <h1 class="text-4xl font-bold my-4">Thanks for subscribing!</h1>
      <p class="text-sm">
        A confirmation email has been sent to <span class="font-bold">{email}</span>.
        Please open it and click the button inside to confirm your subscription.
      </p>
    </div>
    
    <button
      on:click={handleDismiss}
      class="btn variant-filled-surface rounded-md w-full xl:mt-7 mt-5 p-3 text-sm"
    >
      Dismiss message
    </button>
  </div>
</main>


<style>
  @media only screen and (max-width: 930px) {
    main {
      background-color: #dfe0e2;
      padding-bottom: env(safe-area-inset-bottom);
    }
    .card {
      width: 100%;
      height: 100%;
      padding: 20vh 30px 30px 30px;
      border-radius: 0;
      justify-content: space-between;
      align-items: center;
    }
    .card div h1 {
      margin-top: 2rem;
    }
  }

  @media only screen and (930px >= width >= 768px) {
    .card div h1 {
      font-size: 3.2rem;
      margin: 3rem 0 2rem 0;
    }
    .card div p {
      font-size: 1.75rem;
      line-height: 2.3rem;
    }
    .p-3 {
      font-size: 1.5rem;
      padding: 1.75rem;
    }
    .suc-img {
      width: 4rem;
      height: 4rem;
    }
  }
</style>
