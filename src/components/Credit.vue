<template lang="html">
    <section v-if="!credit" class="section">

        <div v-if="sent" class="columns">
            <div class="column is-8 is-offset-2">
                <div class="notification">
                    <p class="subtitle is-5 has-text-centered">Credit sent to {{ email }}!</p>
                </div>
            </div>
        </div>

        <div class="container">
            <div class="columns">
                <div class="column">
                    <h1 class="title is-2 has-text-white has-text-centered">Select the credit</h1>
                </div>
            </div>
            <div class="columns is-multiline">
                <div v-for="(c, index) in creditOptions" :key="index" class="column is-6">
                    <p class="box title is-2 has-text-primary has-text-centered"
                        @click="credit = c">
                        ${{ c }}
                    </p>
                </div>

            </div>
        </div>
    </section>
    <section v-else-if="credit">
        <div class="container">
            <div class="columns">
                <div class="column">
                    <h1 class="title is-2 has-text-white has-text-centered">Selected ${{credit}}</h1>
                </div>
            </div>
            <div class="columns">
                <div class="column is-10 is-offset-1">
                    <div class="field">
                        <div class="control">
                            <input autofocus class="input is-large" type="text" v-model="email" placeholder="Enter Email">
                        </div>
                    </div>
                </div>
            </div>
            <div class="columns">
                <div class="column is-6">
                    <div class="buttons has-addons is-centered">
                        <a @click="resetIt" class="is-small button">Reset</a>
                    </div>
                </div>
                <div class="column is-6">
                    <div class="buttons has-addons is-centered">
                        <a @click="sendCredit" class="is-large button">Send Credit</a>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {
            hubData: {
                submittedAt: null,
                fields: [],
                context: {
                    hutk: "3aea3ab5985f7bc544e847d1f76b5857",
                    pageUri: 'https://credit.vazoola.com',
                    pageName: 'Pubcon Credit',
                },
                skipValidation: true,
            },
            creditOptions: [
                200,
                150,
                100,
                50
            ],
            credit: 0,
            email: null,
            sent: false,
        }
    },

    methods: {
        resetIt() {
            this.credit = 0;
            this.email = null;
        },
        sendCredit() {
            //set timestamp
            this.hubData.submittedAt = Date.now();
            //build hubForm array
              this.hubData.fields.push({
                  name: 'credit',
                  value: this.credit
              })
              this.hubData.fields.push({
                  name: 'email',
                  value: this.email
              })
            var xhr = new XMLHttpRequest();
            xhr.open('POST', 'https://api.hsforms.com/submissions/v3/integration/submit/3379619/8d244d24-de36-4422-8d18-4c46f77a9676', true);
            xhr.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');
            // send the collected data as JSON
            xhr.send(JSON.stringify(this.hubData));
            // eslint-disable-next-line
            xhr.onloadend = (r => {
                this.sendSuccess();
            });
        },

        sendSuccess() {
            this.credit = 0;
            this.sent = true;
            this.timer = setTimeout(() => {
                this.sent = false;
            }, 5000)
        }
    },
    watch: {
        sent(value) {
            if(!value && this.timer) {
                clearTimeout(this.timer)
                this.email = null
            }
        }
    }
}
</script>

<style lang="css">
</style>
