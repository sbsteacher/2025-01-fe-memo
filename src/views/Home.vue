<script setup>
import { reactive, onMounted } from 'vue';
import { HttpService } from '@/services/HttpService';

const httpService = new HttpService();

const state = reactive({
  memos: [],
});

onMounted(async () => {
  state.memos = await httpService.getItems();
});
</script>

<template>
  <div class="memo-list">
    <router-link v-for="m in state.memos" :to="`/memos/${m.id}`" class="item">
      <div class="d-flex pt-3">
        <div class="pb-3 mb-0 w-100">
          <b>{{ m.title }}</b>
          <div>
            <span role="button">삭제</span>
          </div>
        </div>
        <div class="mt-2">{{ m.content }}</div>
      </div>
    </router-link>

    <router-link to="/memos/add" class="add btn btn-light">
      + 추가하기
    </router-link>
  </div>
</template>

<style lang="scss" scoped></style>
