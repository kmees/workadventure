<script lang="typescript">
    import {enableCameraSceneVisibilityStore} from "../Stores/MediaStore";
    import CameraControls from "./CameraControls.svelte";
    import MyCamera from "./MyCamera.svelte";
    import SelectCompanionScene from "./SelectCompanion/SelectCompanionScene.svelte";
    import {selectCompanionSceneVisibleStore} from "../Stores/SelectCompanionStore";
    import {selectCharacterSceneVisibleStore} from "../Stores/SelectCharacterStore";
    import SelectCharacterScene from "./selectCharacter/SelectCharacterScene.svelte";
    import {customCharacterSceneVisibleStore} from "../Stores/CustomCharacterStore";
    import {errorStore} from "../Stores/ErrorStore";
    import CustomCharacterScene from "./CustomCharacterScene/CustomCharacterScene.svelte";
    import LoginScene from "./Login/LoginScene.svelte";
    import Chat from "./Chat/Chat.svelte";
    import {loginSceneVisibleStore} from "../Stores/LoginSceneStore";
    import EnableCameraScene from "./EnableCamera/EnableCameraScene.svelte";
    import VisitCard from "./VisitCard/VisitCard.svelte";
    import {requestVisitCardsStore} from "../Stores/GameStore";

    import type {Game} from "../Phaser/Game/Game";
    import {chatVisibilityStore} from "../Stores/ChatStore";
    import {helpCameraSettingsVisibleStore} from "../Stores/HelpCameraSettingsStore";
    import HelpCameraSettingsPopup from "./HelpCameraSettings/HelpCameraSettingsPopup.svelte";
    import AudioPlaying from "./UI/AudioPlaying.svelte";
    import {soundPlayingStore} from "../Stores/SoundPlayingStore";
    import ErrorDialog from "./UI/ErrorDialog.svelte";
    import VideoOverlay from "./Video/VideoOverlay.svelte";
    import {gameOverlayVisibilityStore} from "../Stores/GameOverlayStoreVisibility";
    import {consoleGlobalMessageManagerVisibleStore} from "../Stores/ConsoleGlobalMessageManagerStore";
    import ConsoleGlobalMessageManager from "./ConsoleGlobalMessageManager/ConsoleGlobalMessageManager.svelte";
    import { peopleMenuVisible } from '../Stores/PeopleStore';
    import PeopleMenu from './People/PeopleMenu.svelte';

    export let game: Game;
</script>

<div>
    {#if $loginSceneVisibleStore}
        <div class="scrollable">
            <LoginScene game={game}></LoginScene>
        </div>
    {/if}
    {#if $selectCharacterSceneVisibleStore}
        <div>
            <SelectCharacterScene game={ game }></SelectCharacterScene>
        </div>
    {/if}
    {#if $customCharacterSceneVisibleStore}
        <div>
           <CustomCharacterScene game={ game }></CustomCharacterScene>
        </div>
    {/if}
    {#if $selectCompanionSceneVisibleStore}
        <div>
            <SelectCompanionScene game={ game }></SelectCompanionScene>
        </div>
    {/if}
    {#if $enableCameraSceneVisibilityStore}
        <div class="scrollable">
            <EnableCameraScene game={game}></EnableCameraScene>
        </div>
    {/if}
    {#if $soundPlayingStore}
    <div>
        <AudioPlaying url={$soundPlayingStore} />
    </div>
    {/if}

    {#if $peopleMenuVisible}
        <div>
            <PeopleMenu />
        </div>
    {/if}
    <!--
    {#if $menuIconVisible}
        <div>
            <MenuIcon  />
        </div>
    {/if}
    -->
    {#if $gameOverlayVisibilityStore}
        <div>
            <VideoOverlay></VideoOverlay>
            <MyCamera></MyCamera>
            <CameraControls></CameraControls>
        </div>
    {/if}
    {#if $consoleGlobalMessageManagerVisibleStore}
        <div>
            <ConsoleGlobalMessageManager game={game}></ConsoleGlobalMessageManager>
        </div>
    {/if}
    {#if $helpCameraSettingsVisibleStore}
        <div>
            <HelpCameraSettingsPopup></HelpCameraSettingsPopup>
        </div>
    {/if}
    {#if $requestVisitCardsStore}
        <VisitCard visitCardUrl={$requestVisitCardsStore}></VisitCard>
    {/if}
    {#if $errorStore.length > 0}
    <div>
        <ErrorDialog></ErrorDialog>
    </div>
    {/if}
    {#if $chatVisibilityStore}
        <Chat></Chat>
    {/if}
</div>
