<script setup>
//p.175
import { reactive } from 'vue';
import { HttpService } from '@/services/HttpService';
import { useRouter } from 'vue-router';

const httpService = new HttpService();

const router = useRouter();

const state = reactive({
    memo: {
        title: '',
        content: ''
    }
});

const submit = () => {
    httpService.addItem(state.memo);
    alert('저장했습니다.');
    router.push({ path: '/' });
}
</script>

<template>
    <form class="detail" @submit.prevent="submit">
        <div class="mb-3">
            <label for="title" class="form-label">제목</label>
            <input type="text" id="title" class="form-control p-3" 
                v-model="state.memo.title">                
        </div>
        <div class="mb-3">
            <label for="content" class="form-label">내용</label>
            <textarea id="content" class="form-control p-3"
                v-model="state.memo.content"></textarea>             
        </div>
        <button class="btn btn-primary w-100 py-3">저장</button>
    </form>
</template>

<style scoped>

</style>