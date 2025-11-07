<template>
    <div class="fixed bottom-6 right-6 z-50">
        <!-- Floating Button -->
        <div @click="toggleMenu"
            class="w-16 h-16 rounded-full bg-yellow-400 flex items-center justify-center shadow-lg cursor-pointer animate-pulse hover:scale-110 transition-transform duration-300">
            <Headphones class="w-8 h-8 text-black " />
        </div>

        <!-- Expanded Menu -->
        <transition name="fade">
            <div v-if="isOpen" class="absolute bottom-20 right-0 flex flex-col items-center space-y-3">
                <!-- WhatsApp -->
                <a href="https://wa.me/923001234567" target="_blank"
                    class="bg-green-500 w-12 h-12 rounded-full flex items-center justify-center shadow-md hover:scale-110 transition-transform">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"
                        class="text-white  fill-current flex itenms-center justify-center w-10 h-10">
                        <path fill="currentColor"
                            d="M380.9 97.1C339-3.5 233.1-32 139.8 15.8 49.2 61.5 4.3 157.3 24.4 254.7L3.4 384.6a12 12 0 0 0 14.7 13.9l127.9-28.3a203.6 203.6 0 0 0 97.5 24.8h.1c117.8 0 213.5-95.7 213.5-213.6a211.3 211.3 0 0 0-26.7-104.3zM230.2 375.1h-.1a168.9 168.9 0 0 1-86.2-23.5l-6.2-3.7-76 16.8 16.2-74.2-4.1-6.6a168.9 168.9 0 1 1 152.4 90.9zm93.9-123.3c-5.1-2.6-30.3-14.9-35-16.6s-8.1-2.6-11.5 2.6-13.1 16.6-16.1 20-5.9 3.8-11 1.3-21.3-7.8-40.6-24.9c-15-13.3-25.1-29.6-28.1-34.6s-.3-7.7 2.3-10.2c2.4-2.4 5.3-6.1 7.8-9.1s3.3-5.1 5-8.6a9.7 9.7 0 0 0-.5-9.2c-1.3-2.6-11.5-27.7-15.8-38s-8.4-8.7-11.5-8.8-6.4-.2-9.8-.2a18.8 18.8 0 0 0-13.5 6.3c-4.6 5-17.7 17.3-17.7 42.1s18.2 48.9 20.8 52.3 35.9 55 87.1 77.2c12.1 5.2 21.6 8.3 29 10.6 12.2 3.9 23.3 3.3 32.1 2 9.8-1.5 30.3-12.4 34.6-24.4s4.3-22.3 3-24.4-4.6-3.7-9.7-6.3z" />
                    </svg>

                </a>

                <!-- Call -->
                <a href="tel:+923001234567"
                    class="bg-blue-500 w-12 h-12 rounded-full flex items-center justify-center shadow-md hover:scale-110 transition-transform">
                    <Phone class="w-6 h-6 text-white" />
                </a>

                <!-- Email -->
                <a href="mailto:info@example.com"
                    class="bg-red-500 w-12 h-12 rounded-full flex items-center justify-center shadow-md hover:scale-110 transition-transform">
                    <Mail class="w-6 h-6 text-white" />
                </a>

                <!-- Messenger -->
                <a href="https://m.me/yourusername" target="_blank"
                    class="bg-indigo-500 w-12 h-12 rounded-full flex items-center justify-center shadow-md hover:scale-110 transition-transform">
                    <MessageSquare class="w-6 h-6 text-white" />
                </a>
            </div>
        </transition>
    </div>
</template>

<script setup>
import { ref } from "vue";
import { Headphones, Phone, Mail, MessageCircle, MessageSquare } from "lucide-vue-next";

const isOpen = ref(false);

const toggleMenu = () => {
    isOpen.value = !isOpen.value;
};
</script>

<style scoped>
@keyframes pulse-glow {
    0% {
        box-shadow: 0 0 0 0 rgba(250, 204, 21, 0.7);
    }

    70% {
        box-shadow: 0 0 25px 10px rgba(250, 204, 21, 0);
    }

    100% {
        box-shadow: 0 0 0 0 rgba(250, 204, 21, 0);
    }
}

.animate-pulse {
    animation: pulse-glow 2s infinite;
}

.fade-enter-active,
.fade-leave-active {
    transition: all 0.4s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
    transform: translateY(10px);
}
</style>
