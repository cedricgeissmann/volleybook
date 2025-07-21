<script>

import { onMount } from 'svelte'

onMount( async () => {
    const baseColors = localStorage.getItem("base-colors")
    document.body.setAttribute("style", baseColors)
})

function pickColor(ev) {
    const lightness = getLightnessFromHey(ev.target.value)
    console.log(lightness)
    const baseColors = `
        --base-color: ${ev.target.value};
        --text-color: ${lightness > 60 ? "black" : "white"}    
    `
    localStorage.setItem("base-colors", baseColors)
    document.body.setAttribute("style", baseColors)
}

function getLightnessFromHey(hex) {
    hex = hex.replace(/^#/, '')

    const r = parseInt(hex.substr(0, 2), 16)
    const g = parseInt(hex.substr(2, 2), 16)
    const b = parseInt(hex.substr(4, 2), 16)

    const brightness = (0.2126 * r + 0.7152 * g + 0.0722 * b) / 255

    return +(brightness * 100).toFixed(2)
}

</script>

<header>Hello
    <label for="color-picker">Base-Color:
        <input type="color" id="color-picker" on:change={pickColor} />
    </label>
</header>
<aside>some content</aside>
<main>
    <h1>Volleybook</h1>
</main>
<footer>Footer</footer>

<style>
aside {
    grid-area: navbar;
    background-color: var(--surface-color);
    height: 100%;
}

main {
    grid-area: main;
}
header {
    grid-area: header;
}
footer {
    grid-area: footer;
}
</style>
