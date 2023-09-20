

<script>
export default {
    props: {
        contacts: { type: Array, deafault: []},
        activeIndex: { type: Number, deafault: -1},
    },
    emits: ["update:activeIndex"],
    methods: {
        updateActiveIndex(index)  {
            this.$emit("update:activeIndex", index);
        }
    }

};
</script>

<template>
    <ul class="list-group">
        <li 
            class="list-group-item"
            v-for="(contact, index) in contacts"
            :key="index"
            :class="{active: index === activeIndex}"
            @click="updateActiveIndex(index)"

        
        
        
        >
        {{  contact.name }}

        </li>
    </ul>
  
</template>