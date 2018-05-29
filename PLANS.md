# Guke

Guke tries to bring Cucumber-style testing to Go in a way that people used to Cucumber will feel at home with, but which also adheres to Go testing idioms.

I'm aware of `godog` and `gucumber`. Both have some nice approaches. This work may turn into a pull request to one of those libraries. They do a great job of working with feature files and providing a very Cucumber-like environment.

What I don't like about them is they depart from Go's testing patterns. `*testing.T` has grown over the years, with the ability to run parallel tests and organize them in suites using the simple `t.Run(...)` method. It's gained coverage tools, growing debugger and IDE support. Numerous matcher libraries offer rich predicates for free. Tests can live alongside benchmarks. Go's own build tools make sure test code is ignored in the executable. The test tool lets you compile tests into their own executable (embedded or templated `.feature`s would be needed to bundle this as a single file) for certain CI and acceptance situations.

I want to use Cucumber (Gherkin) for some kinds of acceptance tests, but I want to stay in the same vein as these maturing tools.

It seems to me there are several broad approaches:

1. Features stay the one source of truth. Guke would provide simple functions to run a feature file as a Go testing function and a `flags` plugin to filter tests. Steps would be written in the typical way, as methods of a `TestWorld` structure. A very slim test world interface would play well with dependency (and mock-dependency) injection. Step association would be through a `Match()` interface or regexp registration function. I do like `gucumber`'s context design.

2. Another way would be to Cuke in code (like the Python library I wrote). This might be a nice option for mature features or lower-level features that will always live as Go code and speak to programmers rather than project owners. This can read pretty nicely, and it offers type checking and easy compilation. It could be templated from the feature files. OTOH, it departs from `.feature` files.
