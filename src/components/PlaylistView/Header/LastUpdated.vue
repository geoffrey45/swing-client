<template>
    <div class="last-updated">
        <span v-if="!isHeaderSmall" class="status">Last updated {{ playlist.info._last_updated }}</span>
        <div v-if="Number.isInteger(playlist.info.id)" class="edit">
            &#160;&#160;|&#160;&#160; <span @click="editPlaylist">Edit</span>&#160;&#160;
            {{ Number.isInteger(playlist.info.id) ? ' | ' : '' }}
            <DeleteSvg class="edit" @click="deletePlaylist" />
        </div>
    </div>
</template>
<script setup lang="ts">
import DeleteSvg from '@/assets/icons/delete.svg'

import { isHeaderSmall } from '@/stores/content-width'

import useModalStore from '@/stores/modal'
import usePStore from '@/stores/pages/playlist'

const playlist = usePStore()
const modal = useModalStore()

function editPlaylist() {
    modal.showEditPlaylistModal()
}

function deletePlaylist() {
    modal.showDeletePlaylistModal(playlist.info.id)
}
</script>

<style lang="scss">
.last-updated {
    position: absolute;
    bottom: 1rem;
    right: 1rem;
    padding: $smaller $small;
    font-size: 0.9rem;
    font-weight: 500;
    border-radius: $smaller;
    z-index: 12;

    display: flex;
    align-items: center;

    .edit {
        display: flex;
        align-items: center;
    }

    .edit > span {
        cursor: pointer;
        color: $brown;
    }

    .edit > svg {
        cursor: pointer;
    }

    svg {
        transform: scale(0.75);
        margin-bottom: -0.2rem;
        color: $red !important;
        height: 1.5rem;
    }
}
</style>
