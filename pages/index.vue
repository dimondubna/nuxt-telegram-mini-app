<script setup lang="ts">
import { ref, onMounted } from 'vue';
import axios from 'axios';
import { useRoute } from 'vue-router';
import { IconChevronRight } from '@tabler/icons-vue';

// تعریف متغیرهای داده‌ها
const token = useRoute().query.token;
const total_token = ref(0);
const username = ref(''); // می‌تونی این رو از سمت سرور بگیری

onMounted(async () => {
  try {
    const response = await axios.get('https://lacewing-learning-externally.ngrok-free.app/api/tokens', {
      headers: {
        Authorization: 'Bearer ' + token,
      },
    });
    total_token.value = response.data.total_tokens;
    username.value = response.data.user;
  } catch (error) {
    console.error('Error fetching token data:', error);
  }
});
</script>

<template>
  <div class="flex flex-col bg-black min-h-screen p-4 text-white">
    <!-- بخش پروفایل -->
    <div class="bg-[#1a1a1a] p-3 rounded-lg flex flex-col justify-between my-8">
        <div class="flex items-center justify-between">
            <div class="flex flex-col gap-1">
                <div class="flex items-center gap-2">
                  <Avatar class="bg-[#35ba75] border-2 border-[#05c964]">
                    <AvatarFallback>
                        {{ username ? username.split('').slice(0, 2).join('').toUpperCase() : '' }}
                      </AvatarFallback>
                  </Avatar>
                    <p class="text-white">{{ username }}</p>
                </div>
            </div>
            <a  class="bg-[#25ff8f] text-black px-4 py-2 rounded-full text-sm">Verify</a>
        </div>
    </div>

    <!-- بخش نمایش توکن و برداشت -->
    <div class="flex flex-col items-center gap-2 mb-8">
      <span class="text-3xl font-bold">{{ total_token ? total_token.toLocaleString() : '0' }}</span>
      <span class="text-xl text-gray-400">Available Tokens</span>
      <Button class="w-full py-4 mt-4 text-lg font-semibold hover:bg-[#25ff8f] bg-[#25ff8f] text-black rounded-xl">
        Withdrawal
      </Button>
    </div>

    <!-- بخش earns -->
    <div class="mt-4">
      <h1 class="text-2xl mb-4">Earnings</h1>
      <div class="flex flex-col gap-4">

        <!-- فالو توییتر-->
        <div class="bg-[#1a1a1a] p-3 rounded-lg flex flex-col justify-between">
            <div class="flex items-center justify-between">
                <div class="flex flex-col gap-1">
                    <div class="flex items-center gap-2">
                        <img src="https://img.icons8.com/color/48/000000/twitter--v1.png" alt="Twitter" class="w-6 h-6" />
                        <p class="text-white">Follow us on Twitter</p>
                    </div>
                    <p class="text-gray-400 mt-2 text-sm">Earn 100 tokens for following</p>
                </div>
                <a href="https://x.com/Depin_Tech" target="_blank" class="bg-[#25ff8f] text-black px-4 py-2 rounded-full text-sm">Follow</a>
            </div>
        </div>
        
        <!-- کانال 2 -->
        <div class="bg-[#1a1a1a] p-3 rounded-lg flex flex-col justify-between">
            <div class="flex items-center justify-between">
                <div class="flex flex-col gap-1">
                    <div class="flex items-center gap-2">
                        <img src="https://img.icons8.com/?size=100&id=63306&format=png&color=000000" alt="Twitter" class="w-6 h-6" />
                        <p class="text-white">Join us on Channel</p>
                    </div>
                    <p class="text-gray-400 mt-2 text-sm">Earn 100 tokens for joining</p>
                </div>
                <a href="https://t.me/DepinTech" target="_blank" class="bg-[#25ff8f] text-black px-4 py-2 rounded-full text-sm">Join</a>
            </div>
        </div>
        
        <!-- کانال 3-->
        <div class="bg-[#1a1a1a] p-3 rounded-lg flex flex-col justify-between">
            <div class="flex items-center justify-between">
                <div class="flex flex-col gap-1">
                    <div class="flex items-center gap-2">
                        <img src="/youtube.png" alt="Youtube" class="w-6 h-6" />
                        <p class="text-white">Subscribe Youtube </p>
                    </div>
                    <p class="text-gray-400 mt-2 text-sm">Earn 50 tokens for subscribe</p>
                </div>
                <a href="https://youtube.com/@depintech/" target="_blank" class="bg-[#25ff8f] text-black px-4 py-2 rounded-full text-sm">Subscribe</a>
            </div>
        </div>

        <NuxtLink :to="{ name: 'earns', query: {token: token} }" class="bg-[#1a1a1a] p-2 rounded-3xl flex gap-1 justify-center items-center text-sm">
            <span>More earnings</span>
            <IconChevronRight stroke="1.5" size="20" color="currentColor" />
        </NuxtLink>
      </div>
    </div>

  </div>
</template>
