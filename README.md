#Griddy McGridface

Griddy McGridface (or short - griddy) is a layout-system based on CSS-grid instead of flex which can be used as alternative and/or addition to flex-based grid-systems like Bootstrap.

## Why

The main motivation behind griddy is to easily break out of the grid (into the void),
and to overlap elements defined in the grid. These two scenarios always include some
hacky workarounds when you come across them in e.g. Bootstrap. While having a single
full-width element not constrained by the grid is one of the simpler tasks, having it
break out in only some specific breakpoints, or only on one side of the grid is much
harder to do.

To overlap two elements in a Bootstrap-like grid horizontally, one could create two
grid-containers, overlapping by setting one of them absolutely positioned,
or some whacky negative-margin-solutions or use transform to place the element. Both
approaches need to replicate the widths/gutters of the grid to accomplish a layout that
still lies within the edges of the columns.

Griddy provides simple utility-classes to create such layouts.

## How

The grid-system consists out of 14 columns instead of 12. The two outermost columns
represent the "void", the space outside of the actual grid. The inner 12 columns replicate
the same columns as Bootstrap (with default variables). The nature of css-grid allows to
easily place elements outside of the 12-column-grid and to overlap them.

## Usage

### Defining the Griddy-Container

All cells that make use of griddy have to be in a griddy-container:

```html
<div class="griddy-container">
    More griddy here
</div>
```

This class actually just sets `overflow-x: hidden;`, because otherwise the grid would
be larger than the page due to it's gutter implementation.

### Defining Griddy

The actual grid-system is implemented in the `.griddy`-class which can be seen like
a `.row` in Bootstrap. Consecutive `.griddy`-elements will be placed beneath each other.

```html
<div class="griddy">
    Your Griddy-Cells
</div>
```

### Defining Cells

All the content is inside `.griddy-cell`-elements. The Bootrap-Analogy would be the `.col`-elements. It makes sure, the actual content aligns with the columns, and here you
can define the positioning of the elements. This class also sets all elements to use the
first grid-row, so they can overlap. However, this can be overridden by the `.griddy-row-{n}` class described later.

### griddy-from

`.griddy-{bp}-from-{void | 1..12}`

With this utility-class, you can define the starting column of a cell:

```
.griddy-from-1 //start at the first column
.griddy-from-5 // start at the 5th column
.griddy-from-void // start from the left edge of the container (breaking out on the left side)

.griddy-sm-from-2 // start from second column, from small breakpoint upwards
.griddy-md-from-3 // start from third column, from medium breakpoints upwards
.griddy-lg-from-4 // start from fourth column, from large breakpoints upwards
.griddy-xl-from-5 // start from the fifth column, from very large breakpointd upwards
```

### griddy-to

`.griddy-{bp}-to-{void | 1..12}`

With this utility-class, you can define the ending column of a cell:

```
.griddy-to-11 //end at the 11th column
.griddy-to-5 // end at the 5th column
.griddy-to-void // end at the right edge of the container (breaking out on the right side)

.griddy-sm-to-2 // end at second column, from small breakpoint upwards
.griddy-md-to-3 // end at third column, from medium breakpoints upwards
.griddy-lg-to-4 // end at fourth column, from large breakpoints upwards
.griddy-xl-to-5 // end at the fifth column, from very large breakpointd upwards
```

### griddy-row

`.griddy-{bp}-row-{1..12}`

With griddy-row, you can explicitely set the vertical ordering of elements. This is
mainly useful for having some of the elements beneath each other on smaller screens,
not overlapping as the default sets it. The limit of 12 rows was chosen "randomly"
to reduce the final css-size.

```
.griddy-row-2 // initially display the element in the second row
.griddy-md-row-1 // but push it up to the other element(s) on medium screens.
```

### Other Utility Classed

#### `.griddy-{bp}-full`

Makes the element span over all 12 main-columns. Shortcut for `.griddy-from-1.griddy-to-12`.

With `.griddy-md-full`, you can make the element use all columns from medium screens upwards.

#### `.griddy-{bp}-void`

Similar to griddy-full, but makes the element span across the whole screen. Also can be
used with breakpoint-infixes.

### Nested Grids

Griddy supports nested grids, with omitting the outermost 2 when nested. This means,
`.griddy-void` is identical with `.griddy-full`, and `.griddy-from-void` with `.griddy-from-1` - and so on.

```html
<div class="griddy-container">
    <div class="griddy">
        <div class="griddy-cell griddy-from-1 griddy-to-8">
            <div class="griddy"> <!-- Nested grid here -->
                <div class="griddy-cell griddy-from-1 griddy-to-6">
                    Cell in a nested Grid
                </div>
                <div class="griddy-cell griddy-from-7 griddy-to-12">
                    Another cell in a nested grid
                </div>
            </div>
        </div>
        <div class="griddy-cell griddy-from-9 griddy-to-12">
            Element in outer grid
        </div>
    </div>
</div>
```

## Is Griddy a replacement for flex-based grids?

**No.** Griddy solves some of the problems of flex-based grids, as breaking out and overlapping elements. However, it also has downsides that'll make working with griddy
exclusively a pain.

### Dynamic rows

You can't define that each element should take up 3 columns and automatically use
the next row, when 4 elements are already inside the grid. Griddy expects explicit definitions of where an element starts and where it ends. This limits the use of griddy
to components/elements that are intended to be used as a single "row" in the page rather than e.g. a dynamic list of tiles.

### Markup-Madness

Writing griddy-definitions, especially responsive ones, makes use of a lot of classes. Each
cell usually expects two classes for each breakpoint, so you can easily end up with
something like

```html
<div class="griddy-cell griddy-row-2 griddy-md-row-1 griddy-from-1 griddy-to-6 griddy-md-from-9 griddy-md-to-void">...</div>
```

## So when to use Griddy

You should use griddy, when

  * you have to break out of the grid on only one side
  * you have to break out on the grid only on specific breakpoints
  * you want elements to overlap each other

When an element is not intended to be used repeatedly in a container and dynamically adjust its rows, griddy can still be used wihtout much headache. But if en element
should be able to do that, use other grid-systems.

```html
<div class="container">
    <div class="row">
        <div class="col-3">1</div>
        <div class="col-3">2</div>
        <div class="col-3">3</div>
        <div class="col-3">4</div>
        <div class="col-3">5</div>
        <div class="col-3">6</div>
        <div class="col-3">Use flex-based grid-systems in such a case</div>
    </div>
</div>
<div class="griddy-container">
    <div class="griddy">
        <div class="griddy-cell griddy-from-void griddy-to-5">
            Use griddy in these cases (breaking out of one side)
        </div>
        <div class="griddy-cell griddy-from-4 griddy-to-12">
            And overlapping with the previous element
        </div>
    </div>
</div>
```