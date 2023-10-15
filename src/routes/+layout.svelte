<script>
    import iconHome from "@iconify-icons/ic/outline-home";
    import iconHomeS from "@iconify-icons/ic/twotone-home";
    import videoLibraryOutlineRounded from '@iconify/icons-material-symbols/video-library-outline-rounded';
    import downloadIcon from '@iconify/icons-material-symbols/download';
    import iconCode from "@iconify-icons/ic/outline-code";
    import { base } from "$app/paths";
    import { page } from "$app/stores";
    import { StyleFromScheme } from "m3-svelte";
    import { FAB } from "m3-svelte";
    import { NavList } from "m3-svelte";
    import { NavListLink } from "m3-svelte";
  
    const paths = [
      {
        path: base || "/",
        icon: iconHome,
        iconS: iconHomeS,
        label: "Home",
      },
      {
        path: base + "/favourite",
        icon: videoLibraryOutlineRounded,
        iconS: videoLibraryOutlineRounded,
        label: "Favourite",
      },
      {
        path: base + "/downloads",
        icon: downloadIcon,
        iconS: downloadIcon,
        label: "Downloads",
      },
    ];
    $: pathNormalized = $page.url.pathname.replace(/\/$/, "") || "/";
  </script>
  
  <StyleFromScheme
  lightScheme={{"primary":4287515953,"onPrimary":4294967295,"primaryContainer":4294958030,"onPrimaryContainer":4281798144,"inversePrimary":4294948248,"secondary":4286011211,"onSecondary":4294967295,"secondaryContainer":4294958030,"onSecondaryContainer":4281079309,"tertiary":4285030192,"onTertiary":4294967295,"tertiaryContainer":4293977000,"onTertiaryContainer":4280359680,"error":4290386458,"onError":4294967295,"errorContainer":4294957782,"onErrorContainer":4282449922,"background":4294965494,"onBackground":4280490518,"surface":4294965494,"onSurface":4280490518,"surfaceVariant":4294303446,"onSurfaceVariant":4283646782,"inverseSurface":4281871914,"inverseOnSurface":4294962663,"outline":4286935917,"outlineVariant":4292395706,"shadow":4278190080,"scrim":4278190080,"surfaceDim":4293449424,"surfaceBright":4294965494,"surfaceContainerLowest":4294967295,"surfaceContainerLow":4294963692,"surfaceContainer":4294765284,"surfaceContainerHigh":4294370526,"surfaceContainerHighest":4294041561,"surfaceTint":4287515953}}
  darkScheme={{"primary":4294948248,"onPrimary":4283768840,"primaryContainer":4285609500,"onPrimaryContainer":4294958030,"inversePrimary":4287515953,"secondary":4293377710,"onSecondary":4282657312,"secondaryContainer":4284301365,"onSecondaryContainer":4294958030,"tertiary":4292134798,"onTertiary":4281872390,"tertiaryContainer":4283385627,"onTertiaryContainer":4293977000,"error":4294948011,"onError":4285071365,"errorContainer":4287823882,"onErrorContainer":4294957782,"background":4279898382,"onBackground":4294041561,"surface":4279898382,"onSurface":4294041561,"surfaceVariant":4283646782,"onSurfaceVariant":4292395706,"inverseSurface":4294041561,"inverseOnSurface":4281871914,"outline":4288712070,"outlineVariant":4283646782,"shadow":4278190080,"scrim":4278190080,"surfaceDim":4279898382,"surfaceBright":4282529587,"surfaceContainerLowest":4279503881,"surfaceContainerLow":4280490518,"surfaceContainer":4280753690,"surfaceContainerHigh":4281477156,"surfaceContainerHighest":4282200623,"surfaceTint":4294948248}} />
  <div class="container">
    <div class="sidebar">
      <NavList type="auto">
        <div class="fab">
          <FAB on:click={() => window.open("https://github.com/KTibow/m3-svelte")} icon={iconCode} />
        </div>
        <div class="items">
          {#each paths as { path, icon, iconS, label }}
            {@const selected = pathNormalized == path}
            <NavListLink type="auto" href={path} {selected} icon={selected ? iconS : icon}>
              {label}
            </NavListLink>
          {/each}
          <!-- <NavListLink
            type="auto"
            href={base + "/transitions"}
            selected={$page.url.pathname.startsWith(base + "/transitions")}
            icon={$page.url.pathname.startsWith(base + "/transitions")
              ? iconAnimationS
              : iconAnimation}
          >
            Animations
          </NavListLink> -->
        </div>
      </NavList>
    </div>
    <div class="content">
      <slot />
    </div>
  </div>
  
  <style>
    .container {
      display: flex;
      min-height: 100vh;
    }
    .sidebar {
      position: sticky;
      align-self: flex-start;
      display: flex;
      width: 5rem;
      flex-shrink: 0;
    }
    .content {
      padding: 1rem;
    }
    @media (max-width: 37.5rem) {
      .container {
        flex-direction: column-reverse;
        --m3-util-bottom-offset: 5rem;
        
      }
      .sidebar {
        bottom: 0;
        left: 0;
        right: 0;
        width: 100%;
        z-index: 3;
      }
      .fab {
        position: fixed;
        right: 1rem;
        bottom: 6rem;
      }
      .items {
        display: contents;
      }
    }
    @media (min-width: 37.5rem) {
      .content {
        flex-grow: 1;
        padding: 1.5rem;
      }
      .sidebar {
        top: 0;
        left: 0;
        flex-direction: column;
        min-height: 100vh;
      }
      .fab {
        display: flex;
        flex-direction: column;
        align-items: center;
        z-index: 2;
        margin-bottom: 1.5rem;
      }
      .fab > :global(button) {
        box-shadow: none !important;
      }
      .items {
        display: flex;
        flex-direction: column;
        gap: 0.75rem;
        justify-content: center;
      }
      @media (min-height: 30rem) {
        .items {
          position: absolute;
          inset: 0;
        }
        @media (max-height: 35rem) {
          .items {
            padding-top: 3.5rem;
          }
        }
      }
    }
  </style>