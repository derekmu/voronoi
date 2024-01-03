# Voronoi diagrams in Go

An implementation of Steven J. Fortune's algorithm to efficiently compute Voronoi diagrams in Go language.

Based on Raymond Hill's javascript implementation: https://raw.github.com/gorhill/Javascript-Voronoi.

Updated with a go.mod file, tagged versions, and stable versions per https://pkg.go.dev.

## Usage

```go
import "github.com/derekmu/voronoi"

func useVoronoi() {
    // Sites of voronoi diagram
	sites := []voronoi.Vertex{
		voronoi.Vertex{4, 5},
		voronoi.Vertex{6, 5},
		...
	}

	// Create bounding box of [0, 20] in X axis
	// and [0, 10] in Y axis
	bbox := NewBBox(0, 20, 0, 10)

	// Compute diagram and close cells (add half edges from bounding box)
	diagram := voronoi.ComputeDiagram(sites, bbox, true)

	// Iterate over cells
	for _, cell := diagram.Cells {
		for _, hedge := cell.Halfedges {
		    ...
		}	
	}

	// Iterate over all edges
	for _, edge := diagram.Edge {
	    ...
	}
}