<script lang="ts">
	import { page } from '$app/state';
	import * as NavigationMenu from "$lib/components/ui/navigation-menu/index.js";
	import { cn } from '$lib/utils';

	let activeUrl = $state(page.url.pathname);
	let loggedIn = $state(true);
	let isAdmin = $derived(loggedIn && false);
    let logInOut = function(){
        loggedIn = !loggedIn
    }
</script>

<header class="flex h-[70px] w-full justify-between">
	<NavigationMenu.Root class="flex justify-self-start" value={activeUrl}>
        <NavigationMenu.List class="flex">
                        
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
        </NavigationMenu.List>
    </NavigationMenu.Root>

    <div class="flex justify-self-end relative">
        <NavigationMenu.Root value={activeUrl}>
            <NavigationMenu.List class={cn("bg-blue-300 items-stretch")}>
                <NavigationMenu.Item class={cn("flex left-0")}>
                    <NavigationMenu.Trigger class={cn("bg-amber-200 hover:bg-amber-300 h-full")}>First</NavigationMenu.Trigger>
                    <NavigationMenu.Content class={cn("bg-red-300")}>
                        <ul class="grid w-[200px] bg-green-300">
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
            </NavigationMenu.List>
        </NavigationMenu.Root>
        <NavigationMenu.Root value={activeUrl}>
            <NavigationMenu.List class={cn("items-stretch")}>
                <NavigationMenu.Item class={cn("flex left-0 ")}>
                    <NavigationMenu.Trigger class={cn("bg-amber-200 hover:bg-amber-300 h-full")}>Second</NavigationMenu.Trigger>
                    <NavigationMenu.Content class={cn("bg-red-300")}>
                        <ul class="grid w-[200px] bg-green-300">
                            <li>
                                <NavigationMenu.Link>
                                    <a href="/about" target="_blank" class="block p-2 hover:bg-gray-100">Sub 3</a>
                                </NavigationMenu.Link>
                            </li>
                            <li>
                                <NavigationMenu.Link>
                                    <a href="/about" target="_blank" class="block p-2 hover:bg-gray-100">Sub 4</a>
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
                            <!-- <a href="/logout" data-sveltekit-preload-data="off" class="flex p-3 hover:bg-gray-100">Log out</a> -->
                            <button onclick={logInOut} class="flex p-3 hover:bg-gray-100">Log Out</button>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    {:else}
                    <NavigationMenu.Item>
                        <NavigationMenu.Link>
                            <!-- <a href="/login" class="flex p-3 hover:bg-gray-100">Log In</a> -->
                            <button onclick={logInOut} class="flex p-3 hover:bg-gray-100">Log In</button>
                        </NavigationMenu.Link>
                    </NavigationMenu.Item>
                    <!-- <NavigationMenu.Item>
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
                    </NavigationMenu.Item> -->
                {/if}
            </NavigationMenu.List>
        </NavigationMenu.Root>
	</div>
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