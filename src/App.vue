<template>
    <div id="app">
        <nav class="level">
            <a href="/" class="level-item">
                <img src="./assets/logo.png" alt="Vazoola" style="height: 50px;">
            </a>
        </nav>
        <credit />
    </div>
</template>

<script>
import Credit from './components/Credit.vue'

export default {
    name: 'app',
    components: {
        Credit
    }
}
</script>

<style lang="sass">
    @import "~bulma/sass/utilities/_all.sass"
    @import "~bulma/sass/base/_all.sass"
    @import "~bulma/sass/grid/_all.sass"
    @import "~bulma/sass/layout/_all.sass"
    @import "~bulma/sass/elements/container.sass"
    @import "~bulma/sass/elements/title.sass"
    @import "~bulma/sass/elements/box.sass"
    @import "~bulma/sass/elements/button.sass"
    @import "~bulma/sass/elements/form.sass"
    @import "~bulma/sass/components/level.sass"
    @import "~bulma/sass/elements/notification.sass"

    html
        height: 100%
    body
        background-color: #56b4d3
        $gradient-top-left: darken(saturate(adjust-hue(hsl(171, 100%, 41%), -10deg), 10%), 10%)
        $gradient-bottom-right: lighten(saturate(adjust-hue(hsl(171, 100%, 41%), 10deg), 5%), 5%)
        background-image: linear-gradient(141deg, $gradient-top-left 0%, hsl(171, 100%, 41%) 71%, $gradient-bottom-right 100%)
        height: 100%
        margin: 0
        background-repeat: no-repeat
        background-attachment: fixed

    .level
        padding: .75em
        background-image: linear-gradient(0deg, #ffffff45 10%, #ffffff6e 30%, #ffffffd1 80%)

    .section
        padding: 2rem 1.5rem
</style>
