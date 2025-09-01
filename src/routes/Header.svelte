 <script lang="ts">
	import { page } from '$app/state';
	import * as NavigationMenu from "$lib/components/ui/navigation-menu/index.js";
	import { cn } from '$lib/utils';

	let activeUrl = $state(page.url.pathname);
	let loggedIn = $state(true);
	let isAdmin = $derived(loggedIn && true);
    let logInOut = function(e:Event){
        e.preventDefault()
        loggedIn = !loggedIn
    }
</script>

<header class="flex h-[70px] w-full">
	<NavigationMenu.Root class="max-w-none z-10" value={activeUrl} viewport={false}>
        <NavigationMenu.List class="justify-between w-screen">
            
            <div class="flex justify-self-start h-full">
                <NavigationMenu.Item class={cn("justify-self-start")}>
                    <NavigationMenu.Link href="/">Logo</NavigationMenu.Link>
                </NavigationMenu.Item>

                {#if isAdmin}
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href="/admin/users">Users</NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href="/admin/projects">Projects</NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href="/admin/subscriptions">Subscriptions</NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href="/admin/plans">Plans</NavigationMenu.Link>
                    </NavigationMenu.Item>
                {:else if loggedIn}
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href="/projects" class={activeUrl == '/projects' && "underline"}>Projects</NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href="/subscriptions" class={activeUrl == '/subscriptions' && "underline"}>Subscription</NavigationMenu.Link>
                    </NavigationMenu.Item>
                {/if}
            </div>

            <div class="flex justify-self-end h-full">
                <NavigationMenu.Item>
                    <NavigationMenu.Trigger class="bg-transparent">First</NavigationMenu.Trigger>
                    <NavigationMenu.Content>
                        <ul class="w-[200px]">
                            <li>
                                <NavigationMenu.Link href="/about" target="_blank" class="sub-nav">Sub 1</NavigationMenu.Link>
                            </li>
                            <li>
                                <NavigationMenu.Link href="/about" target="_blank" class="sub-nav">Sub 2</NavigationMenu.Link>
                            </li>
                        </ul>
                    </NavigationMenu.Content>
                </NavigationMenu.Item>

                <NavigationMenu.Item>
                    <NavigationMenu.Trigger class="bg-transparent">Second</NavigationMenu.Trigger>
                    <NavigationMenu.Content>
                        <ul class="w-[200px]">
                            <li>
                                <NavigationMenu.Link href="/about" target="_blank" class="sub-nav">Sub 3</NavigationMenu.Link>
                            </li>
                            <li>
                                <NavigationMenu.Link href="/about" target="_blank" class="sub-nav">Sub 4</NavigationMenu.Link>
                            </li>
                        </ul>
                    </NavigationMenu.Content>
                </NavigationMenu.Item>

                {#if loggedIn}
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href={isAdmin ? "javascript:void(0)" : "/settings"}>Settings</NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href="/contact">Contact Us</NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link onclick={logInOut} href="/logout" data-sveltekit-preload-data="off">Log out</NavigationMenu.Link>
                    </NavigationMenu.Item>
                    {:else}
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href="/login" onclick={logInOut}>Log In</NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <!-- <NavigationMenu.Item>
                        <NavigationMenu.Link href="/register">Register</NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href="/pricing">Pricing</NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href="/about">About</NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link href="/contact">Contact Us</NavigationMenu.Link>
                    </NavigationMenu.Item> -->
                {/if}
            </div>

        </NavigationMenu.List>
    </NavigationMenu.Root>
</header>

<div class="w-full h-[80px] text-center printable">
    <div class="relative w-full h-[80px] mt-0 bg-foreground z-1" style:--tag="logo-bar"></div>
</div>

<style>
    :global(nav > div),
    :global(nav ul),
    :global(nav ul li),
    :global(nav ul li > a),
    :global(nav ul li > button)
    {
        height: 100%;
        border-radius: 0;
    }
    :global(nav .sub-nav)
    {
        height: 50px;
    }
    :global(nav a[data-navigation-menu-link]){
        justify-content: center;
    }
</style>