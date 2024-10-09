<script>
  import { goto } from '$app/navigation';

  let email = "";
  let emailError = false;
  let showError = false;

  let list = [
    { msg: "Product discovery and building what matters" },
    { msg: "Measuring to ensure updates are a success" },
    { msg: "And much more!" },
  ];

  // Email validation regex
  function validateEmail() {
    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    emailError = !emailPattern.test(email);
    showError = emailError; // Show error only if email is invalid
    
    if (!emailError) {
      // Pass the email as a query parameter
      goto(`/success?email=${encodeURIComponent(email)}`);
    }
  }

  // Clear error when user starts typing
  function handleInput() {
    if (showError) {
      showError = false;
      emailError = false; // Clear the error state when user starts typing
    }
  }
</script>

<main class="w-screen h-screen flex items-center justify-center text-[#222640] overflow-hidden">
  <div class="card p-4 variant-filled w-max h-[80vh] flex justify-between items-center">
    <div class="card-image mb-img hidden w-full h-[40vh] border-none rounded-xl">
      <enhanced:img
        src="../lib/assets/illustration-sign-up-mobile.svg"
        alt=""
        class="img w-full h-full object-cover"
      />
    </div>

    <div class="card-content w-2/4 py-16 px-7">
      <!-- Sign-up form start -->
      <div>
        <h1 class="xl:text-5xl text-4xl font-bold">Stay updated!</h1>
  
        <p class="xl:my-7 my-5 font-medium xl:text-sm text-xs">
          Join 60,000+ product managers receiving monthly updates on:
        </p>
      </div>

      <ul class="list">
        {#each list as listItem, i}
          <li>
            <a
              href="/elements/lists"
              class="flex items-center font-medium xl:text-sm text-xs"
            >
              <span class="badge">
                <enhanced:img
                  src="../lib/assets/icon-success.svg"
                  alt=""
                  class="w-5 h-5"
                />
              </span>
              <span class="flex-auto">{listItem.msg}</span>
            </a>
          </li>
        {/each}
      </ul>

      <form on:submit|preventDefault={validateEmail} class="mt-7">
        <div>
          <label for="Email" class="text-xs font-bold xl:mb-2 mb-1">
            Email address:
          </label>
          <input
            type="text"
            id="Email"
            bind:value={email}
            class="input variant-filled border-surface-200 rounded-md w-full xl:p-4 p-3
              {emailError ? 'border-red-600 bg-red-100 placeholder-red-400' : 'border-gray-300 bg-white placeholder-gray-400'}"
            placeholder="email@company.com"
            on:input={handleInput}
          />
          {#if showError && emailError}
            <p class="text-red-600 text-xs mt-1">Valid email required</p>
          {/if}
        </div>
      
        <button
          type="submit"
          class="btn variant-filled-surface rounded-md w-full xl:mt-7 mt-5 xl:p-4 p-3"
        >
          Subscribe to monthly newsletter
        </button>
      </form>
    </div>
    <div class="card-image dt-img w-2/4 h-full border rounded-xl border-none">
      <enhanced:img
        src="../lib/assets/illustration-sign-up-desktop.svg"
        alt=""
        class="w-full h-full object-cover rounded-lg"
      />
    </div>
  </div>
</main>

<style>
  @media only screen and (max-width: 930px) {
    main {
      overflow-y: auto;
      background-color: #DFE0E2;
      padding-bottom: env(safe-area-inset-bottom);
    }
    .card {
      width: 100%;
      height: 100%;
      flex-direction: column;
      padding: 0;
      border-radius: 0;
      justify-content: flex-start;
    }
    .card-content {
      width: 100%;
      height: 100%;
      padding: 2rem 1rem 1.5rem 1rem;
      display: flex;
      flex-direction: column;
      justify-content: center;
      gap: 1rem;
    }
    .dt-img {
      display: none;
    }
    .mb-img {
      display: block;
    }
    .mb-img .img {
      border-bottom-left-radius: 1rem;
      border-bottom-right-radius: 1rem;
    }
  }

  @media only screen and (max-width: 330px) {
    .card {
      height: max-content;
    }

    .card-content {
      height: 150vh !important;
      padding-bottom: env(safe-area-inset-bottom);
    }
  }

  @media only screen and (930px >= width >= 768px) {
    .card-content {
      height: 100%;
      gap: 2rem;
    }
    h1 {
      font-size: 3.5rem;
    }
    p, span {
      font-size: 1.4rem;
    }
    .card-content {
      padding: 2rem 2rem 1.5rem 2rem;
    }
    .card-content div {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
    ul {
      display: flex;
      flex-direction: column;
      gap: 0.75rem;
    }
    label {
      font-size: 1.3rem;
    }
    input, button, ::placeholder {
      padding: 1.4rem;
      font-size: larger;
    }
  }
</style>
