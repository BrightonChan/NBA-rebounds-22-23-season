# Long range brilliance

A responsive scatterplot implemented with [Svelte](https://svelte.dev) and [D3](https://d3js.org/) showing
minutes played and 3-point field goals made by the best 3-point shooters in NBA history.

Hovering over the chart causes figures to appear. The mouse pointer does not have to be placed over each circle to reveal stats about the corresponding player.
Associated stats will be shown when the pointer is close enough to one of the circles. This feature, which improves the user experience, was implemented with a [quadtree](https://github.com/d3/d3-quadtree).

This project was bootstrapped with the [Svelte app template](https://github.com/sveltejs/template). The player selector was implemented with [svelte-select](https://github.com/rob-balfre/svelte-select).

## Data source

[NBA](https://www.nba.com/stats/)
