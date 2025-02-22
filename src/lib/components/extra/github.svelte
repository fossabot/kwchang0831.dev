<script lang="ts" context="module">
  export const prerender = true
</script>

<script lang="ts">
  export let user = undefined
  export let repo = undefined
  let info: {
    html_url: string
    description: string
    homepage?: string
    owner: { avatar_url: string }
    stargazers_count: any
    license?: { key?: any }
  }

  import { onMount } from 'svelte'
  onMount(async () => {
    info = await (await fetch(`https://api.github.com/repos/${user}/${repo}`)).json()
  })
</script>

<div class="card bg-base-100 !bg-base-200 my-4 ">
  <div class="p-6">
    {#key info}
      {#if info}
        <div class="flex">
          <div class="flex-initial pr-4">
            <div class="card-title mb-6 !text-3xl font-medium">
              <a rel="noopener noreferrer external" target="_blank" href={info.html_url}>
                {user}/
                <span class="font-semibold">{repo}</span>
              </a>
            </div>
            <p class="prose">
              {info.description}
              <br />
              <a rel="noopener noreferrer external" target="_blank" href={info.homepage}>{info.homepage}</a>
            </p>
          </div>
          <img class="flex-initial w-20 h-20 ml-auto rounded-xl" alt="owner_avatar" src={info.owner.avatar_url} />
        </div>
        <div class="-ml-2 card-actions">
          <button class="btn btn-sm btn-ghost">
            <svg
              aria-hidden="true"
              viewBox="0 0 16 16"
              version="1.1"
              data-view-component="true"
              class="inline-block w-4 h-4 mr-2 fill-current">
              <path
                fill-rule="evenodd"
                d="M8 .25a.75.75 0 01.673.418l1.882 3.815 4.21.612a.75.75 0 01.416 1.279l-3.046 2.97.719 4.192a.75.75 0 01-1.088.791L8 12.347l-3.766 1.98a.75.75 0 01-1.088-.79l.72-4.194L.818 6.374a.75.75 0 01.416-1.28l4.21-.611L7.327.668A.75.75 0 018 .25zm0 2.445L6.615 5.5a.75.75 0 01-.564.41l-3.097.45 2.24 2.184a.75.75 0 01.216.664l-.528 3.084 2.769-1.456a.75.75 0 01.698 0l2.77 1.456-.53-3.084a.75.75 0 01.216-.664l2.24-2.183-3.096-.45a.75.75 0 01-.564-.41L8 2.694v.001z" />
            </svg>
            {info.stargazers_count}
          </button>
          {#if info.license}
            <a class="btn btn-sm btn-ghost" href="https://choosealicense.com/licenses/{info.license.key}">
              <svg
                aria-hidden="true"
                viewBox="0 0 16 16"
                version="1.1"
                data-view-component="true"
                class="inline-block w-4 h-4 mr-2 fill-current">
                <path
                  fill-rule="evenodd"
                  d="M8.75.75a.75.75 0 00-1.5 0V2h-.984c-.305 0-.604.08-.869.23l-1.288.737A.25.25 0 013.984 3H1.75a.75.75 0 000 1.5h.428L.066 9.192a.75.75 0 00.154.838l.53-.53-.53.53v.001l.002.002.002.002.006.006.016.015.045.04a3.514 3.514 0 00.686.45A4.492 4.492 0 003 11c.88 0 1.556-.22 2.023-.454a3.515 3.515 0 00.686-.45l.045-.04.016-.015.006-.006.002-.002.001-.002L5.25 9.5l.53.53a.75.75 0 00.154-.838L3.822 4.5h.162c.305 0 .604-.08.869-.23l1.289-.737a.25.25 0 01.124-.033h.984V13h-2.5a.75.75 0 000 1.5h6.5a.75.75 0 000-1.5h-2.5V3.5h.984a.25.25 0 01.124.033l1.29.736c.264.152.563.231.868.231h.162l-2.112 4.692a.75.75 0 00.154.838l.53-.53-.53.53v.001l.002.002.002.002.006.006.016.015.045.04a3.517 3.517 0 00.686.45A4.492 4.492 0 0013 11c.88 0 1.556-.22 2.023-.454a3.512 3.512 0 00.686-.45l.045-.04.01-.01.006-.005.006-.006.002-.002.001-.002-.529-.531.53.53a.75.75 0 00.154-.838L13.823 4.5h.427a.75.75 0 000-1.5h-2.234a.25.25 0 01-.124-.033l-1.29-.736A1.75 1.75 0 009.735 2H8.75V.75zM1.695 9.227c.285.135.718.273 1.305.273s1.02-.138 1.305-.273L3 6.327l-1.305 2.9zm10 0c.285.135.718.273 1.305.273s1.02-.138 1.305-.273L13 6.327l-1.305 2.9z" />
              </svg>
              {info.license.key}
            </a>
          {/if}
          <button class="ml-auto btn btn-sm btn-circle btn-ghost">
            <svg aria-hidden="true" viewBox="0 0 16 16" version="1.1" data-view-component="true" class="w-6 h-6 fill-current">
              <path
                fill-rule="evenodd"
                d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z" />
            </svg>
          </button>
        </div>
      {/if}
    {/key}
  </div>
</div>
