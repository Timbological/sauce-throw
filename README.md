# Sauce Bottle Throw

A browser physics sim of a bottle of sauce being thrown. Single self-contained HTML file —
no build, no dependencies, no network requests.

**[Try it →](https://timbological.github.io/sauce-throw/)**

The sauce is a real 2D SPH fluid (~220 particles, position-based, Clavet et al.) simulated in
the bottle's own reference frame, so gravity, centrifugal, Coriolis and impact-jolt terms fall
out naturally — in free flight the net gravity is zero and the sauce floats. The liquid's
centre of mass feeds back into the rigid body, so a half-full bottle tumbles differently from
a full one.

## What you can change

**Bottle** — four shapes, fill %, viscosity, mass, wall flex (glass → crushable plastic), cap
on/off. **Throw** — speed, angle, release height (up to 50 m), spin, initial tilt. **World** —
gravity, ground bounce and friction, air drag. **View** — sim speed down to 2%, zoom to 40×,
and a timeline you can scrub back through.

Enter throws, Space pauses, ←/→ scrub frame by frame.

## Some things it gets right

- **Viscosity is a yield stress, not just damping.** Above ~70% the sauce holds its shape and
  clings to the glass; hold the bottle upside down uncapped at 80% and it sits there for about
  four seconds before oozing out. Below 50% it pours straight away.
- **Air drag uses the silhouette** the bottle actually presents to the airflow, so a tumbling
  bottle drags ~3× a nose-first one. Drag acts at the geometric centre while weight acts at the
  centre of mass, so it weathervanes.
- **Contacts use warm-started accumulated impulses**, which is why a landed bottle comes to a
  genuine stop instead of buzzing along the ground forever.
- **Wall flex** deforms the outline as a position-based shell; the fluid containment reads the
  deformed wall, so squashing the bottle really does squeeze its contents.

## Known limits

The yield model is global, so two separated blobs in one bottle would rigidly couple. Spilled
droplets get gravity only — no drag, and they don't collide with the bottle. The outline is 12
vertices, so a hard crumple looks faceted. There's no air inside the bottle, so a squeeze only
moves sauce when the sauce is at the neck.
