<script lang="ts">
	import { page } from '$app/state';
	import * as NavigationMenu from "$lib/components/ui/navigation-menu/index.js";
	import { cn } from '$lib/utils';

	let activeUrl = $state(page.url.pathname);
	let loggedIn = true;
	let isAdmin = $derived(loggedIn && false);
</script>

<header class="flex h-[70px] w-full">
	<NavigationMenu.Root class="flex max-w-none w-full" value={activeUrl}>
        <NavigationMenu.List class="flex w-screen justify-between">
                        
            <div class="flex justify-self-start">
                <NavigationMenu.Item class={cn("justify-self-start")}>
                    <NavigationMenu.Link>
                        <a href="/" class="flex p-3 hover:bg-gray-100">Logo</a>
                    </NavigationMenu.Link>
                </NavigationMenu.Item>

                {#if isAdmin}
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/admin/users" class="flex p-3 hover:bg-gray-100">Users</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/admin/projects" class="flex p-3 hover:bg-gray-100">Projects</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/admin/subscriptions" class="flex p-3 hover:bg-gray-100">Subscriptions</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="javascript:void(0)" class="flex p-3 hover:bg-gray-100">Plans</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                {:else if loggedIn}
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/projects" class={cn("flex p-3 hover:bg-gray-100", activeUrl == '/projects' && "underline")}>Projects</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/subscriptions" class="flex p-3">
                                Subscription
                            </a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                {/if}
            </div>

            <div class="flex justify-self-end relative">
                <NavigationMenu.Item class={cn("flex relative left-0 hover:bg-accent nav-container")}>
                    <NavigationMenu.Trigger class={cn("h-full bg-transparent")}>Introduction</NavigationMenu.Trigger>
                    <!-- <span class="bg-blue-300 p-3 relative left-0 top-15 z-10">
                        testing
                    </span> -->
                    <NavigationMenu.Content class={cn("!relative bg-red-300")}>
                        <ul class="grid w-[350px] gap-2 p-4 !relative left-5 bg-green-300">
                            <li>
                                <NavigationMenu.Link>
                                    <a href="/about" target="_blank" class="block p-2 hover:bg-gray-100">Sub 1</a>
                                </NavigationMenu.Link>
                            </li>
                            <li>
                                <NavigationMenu.Link>
                                    <a href="/about" target="_blank" class="block p-2 hover:bg-gray-100">Sub 2</a>
                                </NavigationMenu.Link>
                            </li>
                        </ul>
                    </NavigationMenu.Content>
                </NavigationMenu.Item>

                {#if loggedIn}
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href={isAdmin ? "javascript:void(0)" : "/settings"} class="flex p-3 hover:bg-gray-100">Settings</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/contact" class="flex p-3 hover:bg-gray-100">Contact Us</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/logout" data-sveltekit-preload-data="off" class="flex p-3 hover:bg-gray-100">Log out</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                {:else}
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/login" class="flex p-3 hover:bg-gray-100">Log in</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/register" class="flex p-3 hover:bg-gray-100">Register</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/pricing" class="flex p-3 hover:bg-gray-100">Pricing</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/about" class="flex p-3 hover:bg-gray-100">About</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <a href="/contact" class="flex p-3 hover:bg-gray-100">Contact Us</a>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                {/if}
            </div>
            
        </NavigationMenu.List>
    </NavigationMenu.Root>
	
</header>

<div class="w-full h-[80px] text-center printable">
    <div class="relative w-full h-[80px] mt-0 bg-primary z-1" style:--tag="logo-bar"></div>
</div>

<style>
:global(li.nav-container > span) {
    position: absolute !important;
    left: 0 !important;
}
</style>