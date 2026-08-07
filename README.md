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

**Bottle** — four shapes, fill %, contents rheology, mass, wall flex (glass → crushable
plastic), cap on/off. **Throw** — speed, angle, release height (up to 50 m), spin, initial tilt. **World** —
gravity, ground bounce and friction, air drag. **View** — sim speed down to 2%, zoom to 40×,
and a timeline you can scrub back through.

Enter throws, Space pauses, ←/→ scrub frame by frame.

## Some things it gets right

- **The contents are a Herschel-Bulkley fluid**, tau = tau_y + K*gdot^n, in real units. Presets
  for water, olive oil, honey, tomato sauce, thick ketchup and mayonnaise set literature values,
  or set the yield stress, consistency and flow index yourself. Shear-thinning is real: tomato
  sauce measures ~78 Pa.s while tipping slowly and under 1 Pa.s during a violent throw, so it is
  stiffer than honey at rest and runnier than honey mid-flight.
- **The yield criterion is quantitatively right.** A yield stress can hold a plug of half-width
  R against gravity only if tau_y >= rho*g*R. For this bottle's 12.8 mm neck that is 138 Pa, and
  the sim retains nothing below 138 Pa and ~36% above it. The wall boundary is stress-limited
  by the same constitutive law, which is what makes that threshold resolution-independent.
- **Air drag uses the silhouette** the bottle actually presents to the airflow, so a tumbling
  bottle drags ~3× a nose-first one. Drag acts at the geometric centre while weight acts at the
  centre of mass, so it weathervanes.
- **Contacts use warm-started accumulated impulses**, which is why a landed bottle comes to a
  genuine stop instead of buzzing along the ground forever.
- **Wall flex** deforms the outline as a position-based shell; the fluid containment reads the
  deformed wall, so squashing the bottle really does squeeze its contents.

## Known limits

There is no air in the bottle, so real tomato sauce (tau_y ~24 Pa) drains out of an upturned
open bottle here. Real sauce mostly stays put because air cannot get in past it — the thumb-over-
a-straw effect — not because its yield stress is holding it. By the tau_y >= rho*g*R criterion
alone it should indeed run out of a 62 mm bottle.

Spilled droplets get gravity only — no drag, and they don't collide with the bottle. The
outline is 18 vertices, so a hard crumple looks faceted. Being 2D, the plug criterion is
tau_y >= rho*g*R rather than the tube result rho*g*R/2, so yield thresholds are twice what an
axisymmetric bottle would give.
