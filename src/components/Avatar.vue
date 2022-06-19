<script>
export default {
    name:'Avatar',
    props: {
        avatar: String
    },

    data() {
        return {
            avatarCreated: `https://avatars.dicebear.com/v2/avataaars/${this.avatar}.svg?options[mood][]=happy`,
        }
    },
}
 </script>

<template>
    <img class="object-cover w-full h-full rounded-tl-lg md:w-48" :src="this.avatarCreated" alt="">
</template>


