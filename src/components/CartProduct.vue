<script setup>
import { useFavoritesStore } from "@/stores/favorites";
import { useCartStore } from "@/stores/cart";

const favoritesStore = useFavoritesStore();
const cartStore = useCartStore();
defineProps({
    product: Object,
});
</script>

<template>
    <div class="p-5 bg-slate-100 rounded-4xl flex items-start justify-between gap-10">
        <div class="flex gap-4 flex-1">
            <div class="w-30 h-30 overflow-hidden">
                <img
                    :src="product.imageUrl"
                    alt=""
                    class="w-full h-full object-cover"/>
            </div>
            <div class="pt-2">
                <h3 class="text-xl font-semibold mb-3">
                    {{ product.title }}
                </h3>
                <div class="flex gap-3 items-center">
                    <button
                        @click="favoritesStore.toggleFavorite(product)"
                        class="rounded-4xl bg-white shadow p-3 cursor-pointer hover:scale-110 transition">
                        <svg
                            width="20"
                            height="20"
                            viewBox="0 0 20 20"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg">
                            <path
                                d="M9.99999 18.0417C9.74166 18.0417 9.49166 18.0083 9.28332 17.9333C6.09999 16.8417 1.04166 12.9667 1.04166 7.58332C1.04166 4.95832 3.14166 2.83332 5.73332 2.83332C7.23332 2.83332 8.64999 3.54166 9.99999 4.85832C11.35 3.54166 12.7667 2.83332 14.2667 2.83332C16.8583 2.83332 18.9583 4.95832 18.9583 7.58332C18.9583 12.9667 13.9 16.8417 10.7167 17.9333C10.5083 18.0083 10.2583 18.0417 9.99999 18.0417Z"
                                fill="#263141"/>
                        </svg>
                    </button>
                    <button
                        @click="cartStore.removeFromCart(product.id)"
                        class="rounded-4xl bg-white shadow p-3 cursor-pointer hover:scale-110 transition">
                        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <path d="M4.16666 5.83333H15.6583C15.8912 5.83334 16.1214 5.88214 16.3343 5.97659C16.5471 6.07103 16.7378 6.20903 16.894 6.38168C17.0503 6.55433 17.1686 6.7578 17.2414 6.97898C17.3142 7.20016 17.3398 7.43414 17.3167 7.66583L16.8167 12.6658C16.7755 13.0771 16.5831 13.4584 16.2766 13.7357C15.9702 14.0131 15.5716 14.1667 15.1583 14.1667H7.19999C6.81455 14.1668 6.44097 14.0334 6.14286 13.789C5.84475 13.5447 5.64054 13.2046 5.56499 12.8267L4.16666 5.83333ZM4.16666 5.83333L3.49166 3.13083C3.44651 2.95063 3.34245 2.79067 3.196 2.67638C3.04954 2.56209 2.8691 2.5 2.68332 2.5H1.66666M6.66666 17.5H8.33332M13.3333 17.5H15" stroke="#263141" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                        </svg>
                    </button>
                </div>
            </div>
        </div>
        <div class="pt-2">
            <b class="text-xl">{{ product.price.toLocaleString("ru-RU") }} ₽</b>
        </div>
        <div class="rounded-4xl bg-white p-1 flex items-center">
            <button
                class="cursor-pointer w-10 h-10 font-bold flex items-center justify-center rounded-4xl p-3 hover:bg-slate-200 transition"
                @click="cartStore.updateQuantity(product.id, -1)">
                -
            </button>
            <span class="w-12 text-center">{{ product.quantity }}</span>
            <button
                class="cursor-pointer w-10 h-10 font-bold flex items-center justify-center rounded-4xl p-3 hover:bg-slate-200 transition"
                @click="cartStore.updateQuantity(product.id, 1)">
                +
            </button>
        </div>
    </div>
</template>