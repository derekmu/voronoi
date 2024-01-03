# Voronoi diagrams in Go

An implementation of Steven J. Fortune's algorithm to efficiently compute Voronoi diagrams in Go language.

Based on Raymond Hill's javascript implementation: https://raw.github.com/gorhill/Javascript-Voronoi.

Updated with a go.mod file, tagged versions, and stable versions per https://pkg.go.dev.

## Usage

```go
package main

import (
	"github.com/derekmu/voronoi"
	"log"
)

func main() {
	// Sites of voronoi diagram
	sites := []voronoi.Vertex{
		{X: 4, Y: 5},
		{X: 6, Y: 5},
	}

	// Create bounding box of [0, 20] in X axis and [0, 10] in Y axis
	bbox := voronoi.NewBBox(0, 20, 0, 10)

	// Compute diagram and close cells (add half edges from bounding box)
	diagram := voronoi.ComputeDiagram(sites, bbox, true)

	// Iterate over cells
	for i, cell := range diagram.Cells {
		log.Printf("Cell #%d: %+v", i+1, cell.Site)
		for j, hedge := range cell.Halfedges {
			log.Printf("\tHalf Edge #%d: %+v", j+1, hedge)
		}
	}

	// Iterate over edges
	for i, edge := range diagram.Edges {
		log.Printf("Edge #%d: %+v", i+1, edge)
	}
}

```