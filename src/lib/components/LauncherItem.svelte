<script>
    export let app;

    import { openedApps } from '$lib/store.js';
    import Icon from '@iconify/svelte';

    const check = (appName) => {
            for (let i=0; i<$openedApps.length; i++) {
                if ($openedApps[i].id === appName) {
                    return false;
                    }
                }
    }

    const closeLauncher = () => {
            $openedApps = $openedApps.filter((item) => item.id !== "Launcher");
    }

    const openApp = (App, Name) => {
        if ($openedApps.length === 0 || check(Name) !== false) {
            $openedApps = [...$openedApps, {id: Name, app: App}];
            closeLauncher()
        } else {
            console.log("already opened")
        }
    }
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="item flex flex-col justify-center items-center h-32 w-32 xl:h-40 xl:w-40 text-white rounded relative cursor-pointer transition duration-300 hover:scale-110 active:bg-[#ffffff30]"
on:click={() => openApp(app.component, app.id)}>
    <Icon icon={app.icon} class="h-16 w-16"/>
    <span class="absolute bottom-1 text-sm">{app.id}</span>
</div>