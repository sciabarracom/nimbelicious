<script>

export let api;
import { token } from "./store.js";
let error = "";
let data = {}

async function login() {
  try {
    let res = await fetch(api+"/bookmark/login", {
      method: 'POST',
      body: JSON.stringify(data),
      headers: { "Content-Type": "application/json" }
    })
    res = await res.json()
    error = ""
    if(res.token) {
        token.set(res.token)
    } else if(res.error) {
        error = res.error
    }
  } catch(e) {
    error = e
  }
}
</script>

<div class="container">
    <h1 class="title">Nimbelicious</h1>
    <h1 class="subtitle">Personal Bookmark Manager</h1>
    {#if error}
      <article class="message is-danger">
        <div class="message-header">
          <p>Error</p>
        </div>
        <div class="message-body">
          {error}
        </div>
      </article>
    {/if}
    <div class="field">
        <label for="password" class="label">Type your password</label>
        <div class="control">
            <input size="20" bind:value={data.password} id="password" name="password" class="input" type="password" placeholder="Password">
        </div>
    </div>
    <div class="field">
        <div class="control">
            <button class="button" on:click={login}>Login</button>
        </div>
    </div>
</div>