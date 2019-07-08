#Griddy McGridface

A layout-system based on CSS-grid instead of flex.

## Demo

TODO

## Defining Cells/Columns

Griddy McGridface creates utility-classes similar to Bootstrap with which you can define start and endpoints of a column. Under the hood, the used grid has 14 columns, but the basic utility-classes work with columns 1 to 12, as most people are familiar with.

### griddy-from

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