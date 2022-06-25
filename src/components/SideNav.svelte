<script lang="ts">
  import Icon from '$components/Icon.svelte';
  import { themes } from '$data/themes';
  import { lists } from '$stores/lists.store';
  import NewListButton from './NewListButton.svelte';

  $: listsArr = Object.entries($lists);
</script>

<div class="container">
  <aside>
    <h2>Beautiful Todo</h2>
    <a
      class="source-code"
      href="https://github.com/PuruVJ/ms-todo-svelte"
      target="_blank"
      rel="noopener"
    >
      Source Code
    </a>
    <nav>
      {#each listsArr as [id, { icon, theme, title, type }], i}
        <a
          class:bordered={listsArr.length - 1 !== i && listsArr[i + 1]?.[1]?.type !== type}
          href="/{id}"
          aria-label="{title} list"
        >
          <span class="icon">
            <Icon fill={themes[theme].color} path={icon} />
          </span>
          <span class="title">{title}</span>
        </a>
      {/each}
    </nav>

    <span class="spacer" />

    <NewListButton />
  </aside>
</div>

<style lang="scss">
  .container {
    width: 278px;
    height: 100%;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  aside {
    display: flex;
    flex-direction: column;

    width: 100%;
    height: 100%;

    padding-top: 1rem;

    background-color: #f3f3f3;

    color: var(--app-color-light-contrast);

    position: relative;

    &::before {
      content: '';
      position: absolute;
      height: 16px;
      width: 16px;
      border-radius: 50%;
      top: 0;
      right: -16px;
      box-shadow: -8px -8px #f3f3f3;
    }
  }

  .source-code {
    font-size: 0.7rem;
    text-align: center;
    color: rgba(var(--app-color-dark-rgb), 0.8);

    width: 100%;
  }

  h2 {
    text-align: center;
  }

  nav {
    padding: 0;

    margin: 2rem 0;

    height: 100%;

    display: flex;
    flex-direction: column;
    gap: 4px;
    padding: 4px;

    a {
      display: flex;
      align-items: center;

      text-decoration: none;
      color: var(--app-color-dark);

      border-radius: 4px;

      padding-left: 1rem;

      position: relative;

      // padding: 0.7rem 1rem;

      height: 36px;

      cursor: pointer;

      &:hover {
        background-color: rgb(0 0 0 / 5%) !important;
      }

      &:visited {
        color: var(--app-color-dark);
      }

      &.bordered {
        border-bottom: solid 0.5px rgba(var(--app-color-dark-rgb), 0.3);
      }

      .icon {
        display: flex;
        align-items: center;

        padding-right: 1rem;
      }

      &::before {
        content: '';
        height: 16px;
        width: 3px;
        background: #0067c0;
        border-radius: 3px;
        position: absolute;
        left: 0;
        top: 10px;
      }
    }
  }

  .spacer {
    flex: 1 1 auto;
  }
</style>
