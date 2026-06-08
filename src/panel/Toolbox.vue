<template>
  <div class="flex flex-col gap-0.5">
    <Player />

    <Item type="box">
      <template #title>{{ t`变量管理器` }}</template>
      <template #description>{{ t`查看和管理全局、角色、聊天、消息楼层变量` }}</template>
      <template #content>
        <Button @click="enable_variable_manager = true">{{ t`打开` }}</Button>
      </template>
    </Item>

    <Item type="box">
      <template #title>{{ t`日志查看器` }}</template>
      <template #description>{{ t`查看脚本和渲染界面的控制台日志` }}</template>
      <template #content>
        <Button @click="enable_logger = true">{{ t`打开` }}</Button>
      </template>
    </Item>
  </div>

  <Teleport defer to="#extensionsMenu">
    <div class="extension_container">
      <div
        class="list-group-item flex-container flexGap5 interactable"
        tabindex="0"
        role="listitem"
        @click="enable_variable_manager = true"
      >
        <div class="fa-fw fa-solid fa-square-root-variable extensionsMenuExtensionButton" />
        <span>{{ t`变量管理器` }}</span>
      </div>
      <div
        class="list-group-item flex-container flexGap5 interactable"
        tabindex="0"
        role="listitem"
        @click="enable_logger = true"
      >
        <div class="fa-fw fa-solid fa-file-invoice extensionsMenuExtensionButton" />
        <span>{{ t`日志查看器` }}</span>
      </div>
    </div>
  </Teleport>

  <Dialog
    v-if="enable_variable_manager"
    storage-id="variable-manager"
    :title="t`变量管理器`"
    @close="enable_variable_manager = false"
  >
    <VariableManager />
  </Dialog>
  <Dialog v-if="enable_logger" storage-id="logger" :title="t`日志查看器`" @close="enable_logger = false">
    <Logger />
  </Dialog>
</template>

<script setup lang="ts">
import Logger from '@/panel/toolbox/Logger.vue';
import Player from '@/panel/toolbox/AudioPlayer.vue';
import VariableManager from '@/panel/toolbox/VariableManager.vue';

const enable_variable_manager = ref<boolean>(false);
const enable_logger = ref<boolean>(false);
</script>
