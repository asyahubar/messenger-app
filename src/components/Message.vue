<template>
    <div class="wrapper" :class="{ 'my-message': myMessage }">
        <div class="single-message" :class="{ 'not-read': !message.isRead }">
            <p>{{ message.text }}</p>
            <div class="info" v-if="message.toShowDetails">
                <span>by {{ message.user }} at {{ formattedTime }}</span>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Message',
        props: {
            message: { required: true },
            currentUser: { required: true },
            toShowDetails: { required: false }
        },
        data() {
            return {
                texts: []
            }
        },
        computed: {
            myMessage() {
                return this.currentUser === this.message.user;
            },
            formattedTime() {
                let time = this.message.timestamp;
                time = this.moment(time, 'X')
                    .format('LT');
                return time;
            }
        },
        mounted() {
            this.texts = this.message;
        }
    }
</script>

<style lang="scss">
     .wrapper {
         display: flex;
         min-height: 45px;
     }

     .single-message {
         max-width: 50vw;
         min-width: 10vw;
         width: auto;
         display: block;
         background-color: white;
         border-radius: 10px;
         margin: 10px 8px;
         padding: 8px 16px;
         float: left;
         word-break: break-word;

         p {
             margin: 0;
             padding: 5px 0;
         }

         .info {
             font-size: 11px;
             color: #999;
         }
     }

     .my-message {
         justify-content: flex-end;

         .info {
             float: right;
         }
     }

    .not-read {
        position: relative;

        p::before {
            content: "new";
            color: darkred;
            font-size: 11px;
            position: absolute;
            top: -13px;
            left: 0;
        }
    }
</style>