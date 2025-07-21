<script>

import { onMount } from 'svelte'

onMount( async () => {
    const baseColors = localStorage.getItem("base-colors")
    document.body.setAttribute("style", baseColors)
})

function pickColor(ev) {
    const lightness = getLightnessFromHey(ev.target.value)
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

<header>
    <h1>Volleybook</h1>
    <label for="color-picker">Color:
        <input type="color" id="color-picker" on:change={pickColor} />
    </label>
</header>

<aside>some content</aside>
<main>
    
</main>
<footer>Footer</footer>

<style>
aside {
    grid-area: navbar;
    height: 100%;
    border-right: 2px solid var(--surface-color) ;
}

main {
    grid-area: main;
}

header {
    grid-area: header;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    padding: 0 20px;
    border-bottom: 2px solid var(--surface-color) ;
}

label:has(#color-picker) {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 0.5rem;
}

#color-picker {
    height: 20px;
    width: 20px;
    padding: 0;
    border: var(--text-color) 1px solid;
    border-radius: 50%;
    margin: 0;
}

footer {
    grid-area: footer;
}

</style>
