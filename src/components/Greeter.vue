<template>
    <div>
        <h1 class="mt-5">Hello, {{name}}</h1>
    </div>
</template>

<script>
export default {
    props: [
        'name'
    ],
    data: function () {
        return {
            greeting: 'hello, javi!'
        }
    }
}
</script>

