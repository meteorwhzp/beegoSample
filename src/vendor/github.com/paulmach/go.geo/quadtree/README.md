go.geo/quadtree
===============

Package quadtree implements a quadtree using rectangular partitions.
Each point exists in a unique node; if multiple points are in the same position,
some points may be stored on internal nodes rather than leaf nodes.
This implementation is based heavily off of the 
[d3 implementation](https://github.com/mbostock/d3/wiki/Quadtree-Geom).

## Examples

	func ExampleQuadtreeFind() {
		r := rand.New(rand.NewSource(42)) // to make things reproducible

		qt := quadtree.New(geo.NewBound(0, 1, 0, 1))

		// insert 1000 random points
		for i := 0; i < 1000; i++ {
			qt.Insert(geo.NewPoint(r.Float64(), r.Float64()))
		}

		nearest := qt.Find(geo.NewPoint(0.5, 0.5))
		fmt.Printf("nearest: %+v\n", nearest)

		// Output:
		// nearest: POINT(0.4930591659434973 0.5196585530161364)
	}

	func ExampleQuadtreeInBound() {
		r := rand.New(rand.NewSource(52)) // to make things reproducible

		qt := quadtree.New(geo.NewBound(0, 1, 0, 1))

		// insert 1000 random points
		for i := 0; i < 1000; i++ {
			qt.Insert(geo.NewPoint(r.Float64(), r.Float64()))
		}

		bounded := qt.InBound(geo.NewBound(0.5, 0.5, 0.5, 0.5).Pad(0.05))
		fmt.Printf("in bound: %v\n", len(bounded))
		// Output:
		// in bound: 10
	}
