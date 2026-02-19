# Cargo Bloat Treemap

Interactive single-page treemap visualizer for [cargo-bloat](https://github.com/RazrFalcon/cargo-bloat) JSON output. Displays binary size contributions as a nested treemap where crates, modules, and submodules are represented as hierarchical rectangles — making it easy to spot the biggest contributors to binary bloat at a glance.

Zero dependencies. Single HTML file. Works offline.

## Demo

[Open demo with Wasmi data](https://registry.loopdive.com/users/tt/code/rust/cargo-bloat-treemap/treemap.html?url=wasmi.json)

![Screenshot](screenshot.png)

## Features

- **Nested treemap**: crates > modules > submodules > functions, sized proportionally using a squarify layout
- **Opacity stacking**: each nesting level adds a transparent color layer on the black background — mid-level modules accumulate into richer colors while leaf nodes stay visually distinct
- **Color-coded crates**: each crate gets a distinct hue via golden-angle spacing for maximum visual contrast between neighbors
- **Click to zoom**: click any module to zoom in and fill the view, press Escape or use the breadcrumb trail to navigate back out
- **Hover tooltip**: shows the full Rust path (including trait impls and generics), size in bytes/KB/MB, percentage of text section, and percentage of parent
- **Smart Rust path parsing**: correctly handles `<Type as Trait>::method`, `Fn<T>::method`, closures, and deeply nested module paths
- **Automatic remainder grouping**: items below the threshold are grouped into a `[N smaller items]` block with a distinct striped style — only when the grouped total stays small relative to the parent
- **Adjustable threshold**: slider to control remainder grouping sensitivity (0.5% – 8%)
- **Multiple input methods**: drag & drop, file picker, paste JSON dialog, or `?url=` query parameter
- **Info bar**: shows file size, text section size, function count, and crate count
- **Responsive**: adapts to window resizes
- **Overlapping borders**: child borders sit on top of parent borders to avoid staircase artifacts at deep nesting

## Usage

Generate cargo-bloat JSON:

```sh
cargo bloat --release --message-format=json > bloat.json
```

Then open the visualizer:

- Drag & drop the JSON file onto the page
- Use the "Load JSON" button
- Use the "Paste JSON" button (supports Ctrl+Enter to confirm)
- Or pass it via URL: `treemap.html?url=bloat.json`
