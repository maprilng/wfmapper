# Next Architecture Step

The current release is intentionally still a standalone `index.html`, which keeps it easy to host on GitHub Pages and easy to move between devices.

The next maintainable structure should split the app into folders without changing the user experience:

```text
/
  index.html
  styles/
    base.css
    layout.css
    canvas.css
    modals.css
    guided-start.css
  src/
    app.js
    state/
      graph-store.js
      history.js
      persistence.js
    canvas/
      renderer.js
      hit-testing.js
      layout.js
      interactions.js
    ui/
      guided-start.js
      inspector.js
      toolbar.js
      modals.js
      summary.js
      model-health.js
    domain/
      node-types.js
      flow-types.js
      validation-rules.js
  schemas/
    kbwf.schema.json
  assets/
    icons/
    examples/
```

Recommended migration order:

1. Move CSS out first. This is lowest risk and immediately makes responsive/device work easier.
2. Move constants and schema definitions next, such as node types and flow types.
3. Move pure functions next, such as graph validation, summary generation, and file serialization.
4. Move canvas rendering and hit-testing after tests or visual checks are in place.
5. Keep `index.html` as the stable public entry point so GitHub Pages keeps working.

The immediate iPad fix in this release uses a dynamic viewport height instead of raw `100vh`, plus a mobile viewport meta tag. This should prevent the page from opening slightly shifted under browser UI on iPad Safari.
