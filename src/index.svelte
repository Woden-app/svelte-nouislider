<script>
import { onMount, createEventDispatcher } from 'svelte'
import noUiSlider from 'nouislider'
import 'nouislider/distribute/nouislider.min.css'

export let slider
const dispatch = createEventDispatcher()

export let start
export let connect = false
export let margin
export let limit
export let padding
export let step
export let orientation = 'horizontal'
export let direction = 'ltr'
export let tooltips = false
export let animate = true
export let animationDuration = 300
export let keyboardSupport = true
export let range = {
    min: 0,
    max: 100
}
export let behaviour = 'tap'

onMount(() => {
    noUiSlider.create(slider, {
        start,
        connect,
        margin,
        limit,
        padding,
        step,
        orientation,
        direction,
        tooltips,
        animate,
        animationDuration,
        keyboardSupport,
        behaviour,
        range
    })

    slider.noUiSlider.on(
        'update',
        (values, handle, unencoded, tap, positions) =>
            dispatch('update', { values, handle, unencoded, tap, positions })
    )
    slider.noUiSlider.on(
        'slide',
        (values, handle, unencoded, tap, positions) =>
            dispatch('slide', { values, handle, unencoded, tap, positions })
    )
    slider.noUiSlider.on(
        'set',
        (values, handle, unencoded, tap, positions) =>
            dispatch('set', { values, handle, unencoded, tap, positions })
    )
    slider.noUiSlider.on(
        'change',
        (values, handle, unencoded, tap, positions) =>
            dispatch('change', { values, handle, unencoded, tap, positions })
    )
    slider.noUiSlider.on(
        'start',
        (values, handle, unencoded, tap, positions) =>
            dispatch('start', { values, handle, unencoded, tap, positions })
    )
    slider.noUiSlider.on(
        'end',
        (values, handle, unencoded, tap, positions) =>
            dispatch('end', { values, handle, unencoded, tap, positions })
    )
})
</script>

<div class="slider" bind:this={slider}></div>
