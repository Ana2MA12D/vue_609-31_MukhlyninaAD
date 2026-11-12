<script setup>
import { ref, watch } from "vue";

const props = defineProps({
    modelValue: { type: String, default: "" },
    placeholder: { type: String, default: "Поиск..." },
});

const emit = defineEmits(["update:modelValue"]);

const inputQuery = ref(props.modelValue);

let debounceTimeout = null;

watch(inputQuery, (newVal) => {
    clearTimeout(debounceTimeout);

    if (!newVal.trim()) {
        emit("update:modelValue", "");
        return;
    }

    debounceTimeout = setTimeout(() => {
        emit("update:modelValue", newVal);
    }, 300);
});

watch(
    () => props.modelValue,
    (newVal) => {
        inputQuery.value = newVal;
    },
);

const clearSearch = () => {
    clearTimeout(debounceTimeout);
    inputQuery.value = "";
    emit("update:modelValue", "");
};
</script>

<template>
    <div
        class="flex items-center border px-3 gap-2 bg-white border-gray-500/30 h-[52px] rounded-md">
        <svg
    xmlns="http://www.w3.org/2000/svg"
    width="20"
    height="20"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    stroke-width="2"
    stroke-linecap="round"
    stroke-linejoin="round"
    class="text-gray-400 shrink-0"
>
    <circle cx="11" cy="11" r="8" />
    <path d="m21 21-4.3-4.3" />
        </svg>
        <input
            v-model="inputQuery"
            type="text"
            placeholder="Поиск товаров"
            class="w-full h-full outline-none text-gray-500 placeholder-gray-500 text-sm"
        />
        <button
            v-if="inputQuery"
            class="cursor-pointer"
            @click="clearSearch">
            &times;
        </button>
    </div>
</template>