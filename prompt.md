I have the output of cargo-bloat for my Wasmi application.
Unfortunately cargo bloat only shows a very rough visualization in the form of a line per file or module spanning across over 3000 lines of text.
I thought it would be great if cargo bloat instead visualized the output as a treemap graph where square sizes represent their combined bloat in terms of size relative to the total size.

We likely don't want to visualize all the data points since some affect the binary only marginally.
What I would love to see is this:
top-level squares make up entire crates
next-level squares within those make up the top-level modules
level+1 squares within those make up their sub-modules etc.

Then accumulate their sizes respectively so that a user quickly sees, the biggest offendings crates, their biggest offending modules, and their biggest offending submodules respectively.

I think this is likely the best visual representation for this kind of benchmark.

Can you write me a Python script that reads in JSON like this:
https://gist.github.com/Robbepop/c8805f00d893d23acbbf33868d76146e

And outputs a treemap graph visualization as described above?
Instead of --min-percent I think what would be more suitable is that the visualizer automatically notices when a sub-square would be too tiny for a proper visual representation. If that's the case, the visualizer should put it under a "remainders" sub-quare that is colored slightly distinctly to make the user aware that these are likely not of concern for bloat analysis.
What I may not have specified clearly enough is that sub-squares are important to me. As specified earlier, a square in the treemap is made up of sub-squares of its components, e.g. modules of a crate, submodules of modules etc..
It is important that the user can hover over a square with their mouse to see the code path that represents this square or sub-square.
