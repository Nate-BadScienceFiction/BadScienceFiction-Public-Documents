# THORNBURY CASTLE: MEASURED AKIYABLOCKS SCENE CAMPAIGN

You are the lead geospatial reconstruction engineer, heritage researcher, voxel architect, Akiyablocks scene author, rendering integrator, and verification owner for this campaign.

Your task is to research, implement, bake, register, test, visually validate, and document a new playable Akiyablocks scene named `Thornbury Castle`.

## Campaign identity

Primary scene repository:

    Nate-BadScienceFiction/Akiyablocks-Thornbury

Engine repository:

    Nate-BadScienceFiction/Akiyablocks

Required engine base branch:

    prototype/constructive-distance-lod

Scene key:

    thornbury-castle

Scene label:

    Thornbury Castle

Campaign name:

    THORNBURY_CASTLE_MEASURED_REPLICA

The finished scene must be a metrically grounded, life-sized reconstruction of the present-day Thornbury Castle site in Thornbury, South Gloucestershire, near Bristol, UK. It must include the castle, its registered grounds, and the real-world context extending exactly 100 metres beyond the registered-grounds boundary.

This is also an Akiyablocks scene, not a neutral GIS viewer. Translate the measured site through the visual grammar, material system, scene-package model, level-of-detail machinery, atmosphere controls, and interaction conventions already established by the Akiyablocks engine. The result should feel unmistakably like Thornbury Castle and unmistakably like Akiyablocks.

This is an implementation campaign, not a planning-only exercise. Do not stop after research notes, a speculative architecture proposal, a data download, or a rough footprint extrusion. Complete the scene package, any justified engine support, registration, validation, representative captures, and final evidence.

Do not push changes or open a pull request unless explicitly instructed. Do not overwrite unrelated work.

## Scope of a single run

The campaign spans five gates, each of which is substantial professional work: geospatial acquisition, heritage research, architectural authoring, engine material and profile work, and measured performance. One session will not reach Gate 5, and pretending otherwise produces either sprawl or a fabricated completion claim.

Unless the invoking instruction says otherwise, the deliverable for **this run is Gate 0 and Gate 1**. Complete them to their stated evidence bar, then stop and report: what passed, what the recorded SHAs and baselines are, and precisely what the next run resumes with. That is a successful run, not an early exit.

The prohibition above is against stopping *within* a gate — shipping a plan where geometry was required, or notes where a bake was required. It is not a demand to attempt all five gates at once. If a later run is told to continue, resume from the recorded SHAs and the gate evidence already on disk rather than re-deriving it.

-------------------------------------------------------------------------------
0. AUTHORITY, DECISION ORDER, AND WORKING METHOD
-------------------------------------------------------------------------------

Use the following authority order when instructions conflict:

1. Repository-local instructions and current code on the checked-out branches.
2. Published Akiyablocks architecture, scene-package, SDK, rendering, and test contracts.
3. Legally usable measured evidence and current authoritative source data.
4. This prompt.
5. Convenience.

The current repositories are the source of truth for exact filenames, APIs, package formats, and scripts. This prompt defines required outcomes and architectural constraints. Where an exact path has evolved, use the current established extension point rather than preserving stale wording mechanically.

Work in measured, reviewable gates. For each gate:

- state the player-visible and architectural outcome;
- identify the evidence needed to pass;
- implement the smallest coherent slice;
- run the gate-specific tests and captures;
- repair failures before proceeding;
- record decisions that affect later work.

Do not confuse activity with evidence. A downloaded dataset is not a terrain proof. A screenshot is not a dimensional proof. A unit test is not proof that the scene loaded in the production runtime. A beautiful castle that violates engine contracts is not complete.

-------------------------------------------------------------------------------
1. PRODUCT, FIDELITY, AND AESTHETIC CONTRACT
-------------------------------------------------------------------------------

## 1.1 Canonical site state

Model the present-day extant site using the most recent reliable open data available at implementation time.

Required consequences:

- Model the castle as it now stands, including incomplete and ruined portions.
- Model the roofless outer court as roofless where it is presently roofless.
- Model the surviving inner-court ranges, towers, gatehouses, chimneys, walls, openings, and roof forms.
- Model the present gardens, approaches, lodges, paths, vineyard, hedges, specimen trees, parking access, and nearby context.
- Do not reconstruct the demolished medieval east range as visible default geometry.
- Do not reconstruct the lost two-storey timber gallery or churchyard walkway as visible default geometry.
- Do not reconstruct a conjectural canal, moat, or watercourse.
- Buried or vanished features may be recorded in source metadata or an optional development-only archaeological overlay, but they must not appear in the normal playable scene.
- Never blend present-day and hypothetical Tudor states without an explicit, visible, separately testable mode.

## 1.2 Life-sized metric contract

The intended mapping is:

    1 horizontal world block = 1 real metre
    1 vertical world block   = 1 real metre
    metersPerBlock           = 1
    verticalScale            = 1

Before baking final geometry, verify this mapping against the engine's current player capsule, eye height, collision step, door clearance, stair behavior, camera, and real-world scene conventions. The player must feel human-sized inside the measured site.

If the engine currently assumes a different physical unit in a way that makes a 1 m scene invalid, do not silently distort Thornbury. Identify the exact invariant and implement the smallest generic, documented unit-scale capability needed. That engine change must be reusable, profile- or descriptor-driven where appropriate, default-inert for existing scenes, and covered by regression tests.

Do not resize the castle for drama or to fit an arbitrary box. Preserve true relative positions, orientations, footprints, wall lengths, terrain elevations, road widths, garden dimensions, and building heights within one-block quantisation.

Choose a datum lock and base world Y that:

- leave safe terrain depth below the lowest surface;
- preserve one metre per vertical block;
- leave at least 8 blocks of headroom above the tallest occupied cell;
- keep every emitted structure cell within the current vertical world contract;
- do not clip church towers, castle turrets, chimneys, trees, roofs, or terrain.

### The vertical budget is the first thing that can kill this campaign

The engine's world height is finite and small relative to a life-sized site. On the required base branch:

    src/world/chunk.js:  export const CHUNK_Y = 128

Confirm that value on the branch you actually check out; it is the number that matters, not this quotation of it.

At one metre per vertical block, every term below competes for those blocks:

    terrainDepthBelowLowestSurface        (soil + bedrock under the lowest DTM cell in the AOI)
  + aoiVerticalRelief                     (highest DTM cell − lowest DTM cell across the buffered AOI)
  + tallestStructureAboveItsLocalGround   (church tower is the likely maximum, not a castle turret)
  + 8                                     (required headroom)
  ────────────────────────────────────────
  ≤ CHUNK_Y

Compute this sum in blocks **before authoring any geometry**, and state a source for each term: the DTM crop for the first two, measured or surveyed height for the third. It is a Gate 0 pass condition. Publish it in `IMPLEMENTATION_PLAN.md` as an explicit arithmetic line, not a reassurance.

If the sum does not fit, do not discover that at Gate 3 with a clipped church tower. Stop and report at Gate 0 with the measured terms, and resolve it deliberately — by tightening terrain depth, by justifying a smaller AOI relief through a defensible datum, or, only if genuinely necessary, through the documented generic engine capability §1.2 already permits. Do not resolve it by silently compressing Thornbury's vertical scale, which §13.3 forbids and which would invalidate the entire metric contract.

## 1.3 Exact area of interest

The area of interest, or AOI, is not a radius around a map pin.

Construct it as follows:

1. Obtain the official current polygon for the Thornbury Castle registered park and garden, NHLE entry 1000569.
2. Work in British National Grid, EPSG:27700.
3. Validate and repair the polygon if required without materially changing its boundary.
4. Buffer that polygon outward by exactly 100.0 metres using a projected planar buffer.
5. Use the resulting polygon as the geometric AOI.
6. Compute its exact area, perimeter, bounding box, source date, and source identifier.
7. Expand DEM and chunk bounds only as needed for raster sampling, meshing aprons, and chunk alignment.
8. Clip authored roads, water, buildings, walls, vegetation, and other physical content to the true buffered AOI.
9. Distant horizon rendering may represent geography beyond the AOI, but no playable structure or road geometry may masquerade as measured 100 m context.

If the NHLE service exposes the registered landscape through a dedicated layer, discover and use the correct feature layer. Do not trace the quick-reference web map.

## 1.4 Interior scope

Exterior geometry and exterior traversal are required.

Do not fabricate private hotel interiors. Implement an interior only when all of the following are true:

- a reliable measured plan or authoritative survey supports it;
- the source licence permits use;
- the layout can be represented without speculative room invention;
- it is necessary for a defined player route or acceptance requirement.

Otherwise:

- preserve supported exterior entrances and window positions;
- keep private building volumes collision-solid;
- make courtyards, roofless ruins, gateways, garden compartments, and exterior routes traversable;
- do not create doors leading into blank cavities or invented mazes.

## 1.5 Aesthetic north star

The scene should not chase photorealism. It should produce a measured, painterly, constructive interpretation of Thornbury using the engine's own visual language.

The desired impression is:

- broad, world-locked material marks rather than pasted photographic textures;
- strong architectural masses and value grouping before ornamental detail;
- precise landmark silhouettes at distance;
- legible block construction at close range;
- restrained, site-specific colour rather than generic fantasy-castle grey;
- damp Cotswold limestone, pale mortar, dark yew, deep lawn, lead, stone slate, clay tile, and warm brick chimney accents;
- a distinctly English garden and overcast-west-country atmosphere without forcing permanent gloom;
- selective detail that clarifies ashlar, rubble, roof, ruin, gate, path, hedge, and tree families;
- an impressionistic treatment that never changes measured geometry or disguises traversable space.

The aesthetic must be developed through devices and approaches already used by Akiyablocks, including where applicable:

- scene-selected atmosphere palettes;
- `painterlyProfile` or its current equivalent;
- the branch's constructive-distance LOD grammar;
- semantic face or surface-style data already carried by the mesher;
- world-space procedural material marks;
- existing AO and sky-visibility lighting;
- existing material partitions and shader patching strategy;
- fog, clouds, sky, and horizon profiles;
- deterministic block and position hashing;
- existing UI swatch and target-highlight conventions;
- the production visual-capture harness.

Do not solve the art direction by importing a second renderer. In particular, do not introduce:

- a Thornbury-only renderer fork;
- scene-key branches in shaders, meshing, lighting, input, or world code;
- a permanent fullscreen post-process merely to create style;
- screen-space noise that swims over geometry;
- camera-dependent brush marks that crawl while moving;
- a high-resolution texture atlas that bypasses block identity and swatches;
- unlicensed photographic textures or photogrammetry;
- thousands of tiny ornamental cubes whose only effect is shimmer;
- a generic medieval asset kit that erases the measured site;
- Southwestern adobe, red-rock, or desert colour language inherited accidentally from other scenes.

At near range, openings, wall thickness, roof steps, material families, target highlights, and player affordances must remain clear. At middle range, courts, towers, roof groups, garden walls, lodges, and church must read as coherent masses. At far range, retain the castle silhouette, church tower, principal trees, enclosing walls, and approach geometry without flicker or detail soup.

Create an explicit style brief before the full material pass:

    design-docs/thornbury-castle/AESTHETIC_DIRECTION.md

It must contain:

- five or fewer governing visual principles;
- the site-specific palette and value hierarchy;
- the material families and their gameplay distinctions;
- near, middle, and far-distance rules;
- day, overcast, dusk, and night intent;
- a list of visual approaches deliberately rejected;
- representative proof views;
- measurable acceptance criteria for motion, phone readability, and landmark recognition.

-------------------------------------------------------------------------------
2. TWO-REPOSITORY OWNERSHIP AND ENGINE ARCHITECTURE
-------------------------------------------------------------------------------

Architecture and modularity are acceptance criteria, not cleanup work deferred until the scene looks finished.

## 2.1 Repository ownership

`Akiyablocks-Thornbury` owns scene-specific authorship:

- research and source provenance;
- raw-data fetch and cache orchestration;
- geospatial normalisation;
- measurement ledgers and assumptions;
- Thornbury site plans and semantic feature data;
- castle, church, lodge, garden, vegetation, and context compilers;
- scene-package bake scripts;
- generated package artifacts under the external scene-package contract;
- scene-specific validation and capture definitions where the contract permits them;
- scene documentation and implementation report.

`Akiyablocks` owns general engine capabilities:

- runtime scene-package loading and stamping;
- manifest, cells, structures, and sidecar schemas;
- the curated scene SDK;
- block identities and generic material families;
- meshing, rendering, lighting, LOD, persistence, collision, raycasting, UI swatches, and capture infrastructure;
- generic descriptor fields, accessors, validators, and profile registries;
- the engine-side scene registration descriptor and explicit registry entry when required by the current branch;
- regression tests for engine-wide behavior.

A scene-specific registration descriptor or profile record may name `thornbury-castle`. General algorithms may not contain Thornbury coordinates, feature IDs, castle-part names, or branches on the Thornbury scene key.

## 2.2 Dependency and layering contract

The scene repository must consume the engine only through its documented public authoring surface:

    akiya-blocks/scene-sdk
    akiya-blocks/scene-sdk/node

Do not import from `../Akiyablocks/src/...`, `../Akiyablocks/modules/...`, or other deep engine paths merely because the repositories are siblings. Do not copy engine utilities into the scene repository.

If a needed capability is not exported:

1. determine whether it is genuinely reusable and belongs in the engine;
2. implement or expose the smallest general capability in `Akiyablocks`;
3. preserve the curated export boundary rather than using `export *` casually;
4. document the contract;
5. pin the public export with tests;
6. consume it from `Akiyablocks-Thornbury` through the SDK.

Respect the engine layering rules. In particular:

- runtime `src/` code must not import scene-bake `tools/` code;
- browser-safe SDK exports must not pull Node, DOM, or Three.js dependencies into pure modules;
- Node-only file helpers remain in the Node SDK entry;
- engine code must never import the Thornbury repository;
- scene compilers may produce data for the engine but may not reach into runtime internals;
- pure geometry, projection, and validation modules should remain pure and deterministic;
- one source of truth must own each format string, validator, coordinate convention, and material identity.

## 2.3 Rules for general engine changes

Prefer existing contracts and composition before adding engine code. Add a general capability only when the scene cannot be implemented cleanly through the current SDK, descriptor, package, profile, block, or sidecar contracts.

Before every engine change, record a brief decision answering:

- What scene requirement cannot be expressed through the current contract?
- Which architectural layer owns the missing capability?
- Is this reusable by another measured town, castle, church, garden, or heritage scene?
- Can it be expressed as data or a named profile rather than a scene-key branch?
- Is the default behavior unchanged for all existing scenes?
- What public contract, validator, accessor, or SDK export is required?
- What unit, contract, regression, browser, and phone tests prove it?
- What is the rollback path?

Put these decisions in:

    design-docs/thornbury-castle/ENGINE_DECISIONS.md

Any new general engine module must:

- have one clear responsibility;
- use established naming and directory conventions;
- avoid duplicating an existing helper;
- accept generic data rather than Thornbury constants;
- be deterministic where world generation or rendering identity depends on it;
- be default-inert or backward-compatible;
- fail loudly at contract boundaries rather than silently falling back to a misleading result;
- include focused tests and relevant documentation;
- preserve build, typecheck, lint, runtime lifecycle, save, reset, context restoration, and phone behavior.

Do not over-generalise speculative abstractions. Generalise at a real contract seam, not around the fact that one castle has a tower.

## 2.4 Rendering architecture contract

Rendering extensions must follow the current branch architecture:

- scene data selects registered profiles;
- profiles provide numeric or semantic values;
- shaders and render systems consume profile values, not scene-key strings;
- block or semantic surface identity survives recolouring;
- no RGB-signature routing for new general material families;
- no new chunk partition unless its draw-call and memory cost are measured and justified;
- prefer extending the established dominant-material patch or semantic face channel over forking the lighting model;
- preserve AO, sky visibility, local lights, target highlights, building edits, remeshing, capture, resize, prewarm, teardown, and context restoration;
- do not change persistence or collision for a purely visual feature;
- player-placed blocks must receive the correct material treatment immediately and deterministically.

If a new material family is required, it must be generic, reusable, registered once, available to UI swatches, placeable and breakable where appropriate, and test-pinned through sync and worker meshing paths.

## 2.5 Cross-repository change discipline

When both repositories change:

1. implement and test the engine contract first;
2. commit the engine change as a coherent reusable unit;
3. update the scene repository against that exact engine SHA;
4. implement the scene consumer;
5. run cross-repository integration and package verification;
6. record both SHAs and the dependency relationship.

Do not leave the scene depending on uncommitted engine state. Do not hide a scene-specific engine workaround in an unrelated renderer file.

-------------------------------------------------------------------------------
3. REPOSITORY SAFETY, BASELINES, AND INITIAL MAPS
-------------------------------------------------------------------------------

Before editing either repository:

1. Run and record:

       git status --short
       git branch --show-current
       git rev-parse HEAD
       git remote -v
       git fetch origin

2. Confirm the engine base exists:

       origin/prototype/constructive-distance-lod

3. Preserve unrelated work. If a worktree is dirty, identify ownership before touching overlapping files.

4. Use coherent feature branches based on the correct repository state. A reasonable convention is:

       Akiyablocks-Thornbury: feat/measured-thornbury-castle
       Akiyablocks:           feat/thornbury-generic-support

   Do not create the engine branch unless engine changes are actually required.

   **This instruction is outranked in the engine repository.** `Akiyablocks/CLAUDE.md`
   says, in as many words: *"Never create a git branch automatically — ask first...
   This overrides any default 'branch first on the default branch' behavior."* By the
   authority order in section 0, that repository-local instruction is rank 1 and this
   prompt is rank 4. So in `Akiyablocks`: **ask before creating the branch, and wait for
   explicit confirmation.** Asking is the correct behaviour here, not a stall. The
   scene repository has no such rule; branch there normally unless its own repository
   instructions say otherwise — check them first.

5. Record the exact base SHA for both repositories.

6. Read all repository-level instructions completely, including any `CLAUDE.md`, `AGENTS.md`, README files, package scripts, architecture documents, and test conventions.

At minimum inspect the current engine versions of:

    package.json
    design-docs/project-structure.md
    design-docs/world-core.md
    design-docs/scene-sdk-reference.md
    design-docs/scene-packages.md
    design-docs/scene-registration.md
    design-docs/rendering-and-visuals.md
    design-docs/painterly-rendering-prototypes.md
    tools/scene-sdk/index.mjs
    tools/scene-sdk/node.mjs
    tools/scene-bake/
    modules/dem/
    src/world/scenePackageScene.js
    src/world/scenePackages.js
    src/world/registered-games/middle-place.game.js
    src/world/blocks.js
    src/render/
    tools/visual-capture/
    tests/

Use the branch's current filenames if any have moved. Two documents this prompt
previously named — `design-docs/constructive-block-print-art-direction.md` and
`design-docs/constructive-block-print-technical-plan.md` — are **not present** on the
required base branch; the first was deleted from it and the second never existed under
that name. The live art-direction and rendering references are
`design-docs/rendering-and-visuals.md` and
`design-docs/painterly-rendering-prototypes.md`. If a path in this prompt does not
resolve, record that as a finding in the plan rather than searching indefinitely or
inventing a replacement.

Run clean baselines in both repositories using their lockfiles and documented commands. Prefer `npm ci` when a compatible lockfile exists; otherwise use the repository's normal install command. In the engine, record at least:

    npm run lint
    npm run typecheck
    npm test
    npm run build

If a baseline command already fails, isolate and report the pre-existing failure. Do not claim it as campaign work, and do not use it to excuse new untested failures.

**`npm run typecheck` is expected to fail on the engine baseline.** It emitted 330
errors across 79 files on the required base branch, and `tsconfig.json` is not wired
into CI. Record the exact error count and the offending file set as the Gate 0
baseline. Everywhere this prompt requires typecheck to "pass", the requirement is
**no new errors relative to that recorded baseline**, and no new error in any file this
campaign touches. Do not attempt to fix the 330 pre-existing errors: that is unrelated
work, it is not in scope, and it will consume the campaign.

Before implementation, create:

    design-docs/thornbury-castle/IMPLEMENTATION_PLAN.md

It must include:

- base SHAs and working branches;
- the two-repository ownership matrix;
- scene-package, SDK, DEM, cells, structures, registration, palette, painterly-profile, LOD, capture, and verification extension points found on the branch;
- expected files by repository;
- raw-data caching strategy;
- source licences;
- coordinate transform and proposed origin;
- expected block, chunk, and Y bounds;
- proposed material and aesthetic strategy;
- any proposed engine changes and why existing contracts are insufficient;
- core geometric, licensing, visual, and performance risks;
- acceptance tests and staged gates.

Keep the plan concrete. Update it only when implementation discoveries materially change the design.

-------------------------------------------------------------------------------
4. RESEARCH AND SOURCE PROVENANCE
-------------------------------------------------------------------------------

Research is part of implementation. Do not rely on one map, one tourist photograph, or an automatic OpenStreetMap extrusion.

## 4.1 Source hierarchy by purpose

Heritage identity, boundaries, descriptions, and statutory anchors:

1. Historic England National Heritage List for England.
2. Historic England open GIS datasets and APIs.
3. South Gloucestershire Historic Environment Record where openly accessible.
4. Published archaeological reports and measured historic surveys.

Terrain and heights:

1. Environment Agency 1 m time-stamped DTM and DSM where available.
2. Environment Agency 1 m composite DTM and DSM.
3. Other open British elevation data only as a documented fallback.

Current footprints, roads, paths, access, land cover, and hydrography:

1. OS OpenMap Local and other appropriately licensed OS OpenData.
2. OpenStreetMap, with full ODbL attribution and source date.
3. LiDAR-derived edges and height differences.
4. Current openly licensed orthophotography or aerial imagery where legally reusable.
5. Photographs as visual corroboration, not as an unmeasured map.

Architecture and façade proportions:

1. Current LiDAR and surveyed footprints.
2. Authoritative measured plans and elevations.
3. Public-domain Pugin drawings and other measured historic documents, corrected for known later alterations.
4. Historic England descriptions.
5. Multiple current photographs with perspective-aware measurement.
6. Clearly recorded inference only when stronger evidence is unavailable.

Never use Google Maps, Google Earth, Bing imagery, hotel photography, user-contributed Historic England images, or copyrighted plan scans as redistributable source assets unless the licence expressly permits it. They may be viewed as references where terms allow, but must not be checked in or transformed into an unlicensed derivative dataset.

## 4.2 Mandatory official anchors

Research and preserve these identifiers:

- Registered park and garden:
  - NHLE 1000569
  - https://historicengland.org.uk/listing/the-list/list-entry/1000569
  - NGR ST 63373 90698

- Thornbury Castle inner court:
  - NHLE 1128788
  - https://historicengland.org.uk/listing/the-list/list-entry/1128788
  - retrieve and verify its official NGR and geometry

- Outer court and kitchen-court walls:
  - NHLE 1321132
  - https://historicengland.org.uk/listing/the-list/list-entry/1321132
  - NGR ST6331490720

- Walls enclosing the privy and goodly gardens:
  - NHLE 1312668
  - https://historicengland.org.uk/listing/the-list/list-entry/1312668
  - NGR ST6343390678

- Scheduled buried remains:
  - NHLE 1410041
  - https://historicengland.org.uk/listing/the-list/list-entry/1410041
  - NGR ST6343390703

- West Lodge and gateway:
  - NHLE 1136690
  - https://historicengland.org.uk/listing/the-list/list-entry/1136690
  - NGR ST6334190602

- East Lodge:
  - NHLE 1321107
  - https://historicengland.org.uk/listing/the-list/list-entry/1321107
  - NGR ST6347990662

- Church of St Mary the Virgin:
  - NHLE 1128789
  - https://historicengland.org.uk/listing/the-list/list-entry/1128789
  - NGR ST 63400 90620

Use identifiers as control points and semantic anchors, not substitutes for complete footprints.

## 4.3 Mandatory dimensional cross-checks

Test the constructed scene against documented dimensions including:

- western approach drive approximately 100 m;
- garden walls approximately 4 to 5 m high, with the eastern portion about 1 m lower;
- bee-boles approximately 1 m above ground and spaced approximately 4 m apart;
- north outer-court wall continuing east approximately 87 m as the former kitchen-court wall;
- connecting courtyard face continuing south approximately 13 m;
- current arrangement of inner court, outer court, privy garden, and goodly garden.

These are checks, not excuses to replace measured geometry with rectangles.

## 4.4 Open-data starting points

Historic England NHLE API catalogue:

    https://www.api.gov.uk/he/national-heritage-list-for-england-nhle/

Historic England ArcGIS endpoint:

    https://services-eu1.arcgis.com/ZOdPfBS3aqqDYPUQ/arcgis/rest/services/National_Heritage_List_for_England_NHLE_v02_VIEW/FeatureServer

Environment Agency 1 m composite DTM:

    https://environment.data.gov.uk/dataset/13787b9a-26a4-4775-8523-806d13af58fc

OS OpenMap Local:

    https://www.ordnancesurvey.co.uk/products/os-open-map-local

OpenStreetMap licence and attribution:

    https://www.openstreetmap.org/copyright

Pugin, Examples of Gothic Architecture, second series:

    https://openlibrary.org/works/OL15353417W/Examples_of_Gothic_architecture

Discover current download endpoints rather than hard-coding transient signed URLs.

## 4.5 Provenance artifacts

Create in the scene repository:

    tools/scene-bake/thornbury-castle/data/source-lock.json
    design-docs/thornbury-castle/SOURCES.md
    design-docs/thornbury-castle/MEASUREMENT_LEDGER.csv
    design-docs/thornbury-castle/ASSUMPTIONS.md

For every source record:

- stable source ID;
- title;
- publisher;
- URL or API endpoint;
- retrieval date and time;
- source-data or survey date;
- CRS;
- licence;
- attribution text;
- local cache filename;
- byte count;
- SHA-256;
- whether raw data may be redistributed;
- transformations applied;
- derived outputs depending on it.

The measurement ledger must include at least:

    feature_id
    component
    measurement_name
    value
    unit
    geometry_source
    source_id
    method
    confidence
    uncertainty_m
    checked_by
    notes

Confidence classes:

- A: directly surveyed, LiDAR-derived, or authoritative measured drawing.
- B: corroborated by at least two independent reliable sources.
- C: inferred from one source, photographs, or architectural pattern.
- U: unresolved and intentionally not modelled.

Do not silently promote C-quality inference into A-quality prose or geometry.

## 4.6 Raw-data policy

- Put downloaded GeoTIFFs, archives, temporary GeoJSON, and large raw files in a git-ignored cache.
- Do not commit large raw LiDAR tiles.
- Commit compact deterministic derived data only when the licence permits it.
- Make fetch and derive stages repeatable.
- Support offline rebake from a populated cache.
- Fail with a clear source-specific error when required data is absent and retrieval is unavailable.
- Never embed credentials or API keys.
- Use environment variables for optional authenticated sources.
- Keep generated timestamps out of deterministic package identity.

-------------------------------------------------------------------------------
5. GEODETIC AND WORLD-SPACE CONTRACT
-------------------------------------------------------------------------------

Use EPSG:27700 for measurement, intersection, clipping, buffering, and error calculation.

Choose a stable BNG origin near the AOI centre, preferably rounded metre coordinates. Record:

    originEasting
    originNorthing
    originElevationODN
    baseWorldY
    metersPerBlock
    verticalScale
    EPSG
    WGS84 manifest centre

Use the Akiyablocks axis convention:

- +X east;
- +Z south;
- +Y up.

For BNG coordinates:

    wx = (easting - originEasting) / metersPerBlock
    wz = (originNorthing - northing) / metersPerBlock

For elevation:

    wy = baseWorldY + round((elevationODN - originElevationODN) * verticalScale)

Retain floating-point source geometry through clipping, measuring, and validation. Rasterise only at the final voxel boundary.

Use shared engine SDK mapping and terrain-floor helpers where they express the contract. Do not create a conflicting Thornbury-only coordinate convention.

Add tests for:

- BNG to world transform;
- inverse transform;
- WGS84 control-point conversion;
- +X east and +Z south orientation;
- metre-scale round trips;
- datum-lock stability;
- exact 100 m buffer;
- chunk bounds;
- vertical headroom;
- player-scale plausibility.

Maximum pre-voxelisation round-trip error:

    0.01 m

Maximum control-point residual after voxelisation:

    1 block

-------------------------------------------------------------------------------
6. DETERMINISTIC DATA AND AUTHORING PIPELINE
-------------------------------------------------------------------------------

Build a deterministic staged pipeline separating acquisition, normalisation, measurement, authored interpretation, baking, and validation.

A reasonable scene-repository structure is:

    tools/scene-bake/thornbury-castle.mjs
    tools/scene-bake/thornbury-castle/
        config.mjs
        fetchSources.mjs
        projections.mjs
        buildAoi.mjs
        terrain.mjs
        footprints.mjs
        roads.mjs
        hydrology.mjs
        vegetation.mjs
        heritageAnchors.mjs
        castleGeometry.mjs
        churchGeometry.mjs
        contextGeometry.mjs
        rasterize.mjs
        materials.mjs
        validate.mjs
        report.mjs
        data/

Adapt names to current repository conventions. Do not create a miniature framework where the SDK or shared scene-bake helpers already solve the problem.

Required stages:

1. Fetch or read cached sources.
2. Verify hashes and licences.
3. Reproject to EPSG:27700.
4. Retrieve and validate the registered-grounds polygon.
5. Construct the exact 100 m AOI.
6. Crop the 1 m DTM and useful DSM coverage.
7. Establish the stable vertical datum mapping.
8. Load roads, paths, hydrography, land cover, boundaries, and building data.
9. Reconcile geometry against LiDAR and heritage anchors.
10. Build explicit measured geometry for the castle complex.
11. Build the church and lodges at landmark fidelity.
12. Build context structures at measured-footprint fidelity with simplified façades.
13. Build structural gardens and vegetation.
14. Rasterise terrain, surfaces, water, walls, roofs, structures, and vegetation.
15. Encode documented Akiyablocks package layers using SDK contracts.
16. Produce numerical validation and a bake report.
17. Verify the package with the production verifier.
18. Register and load through the normal runtime.
19. Capture and inspect canonical views in motion and stills.

No stage may depend on `Math.random`, current time, source iteration order, locale-dependent sorting, or machine-specific directory ordering. Hash decorative variation from stable source IDs and coordinates.

Keep authoring semantics richer than runtime voxels where useful. A source record may retain role, district, material family, confidence, and provenance for validation, but emit only the package fields supported by the runtime contract. Do not smuggle compiler-only semantics into runtime assumptions.

-------------------------------------------------------------------------------
7. TERRAIN, ROADS, HYDROLOGY, AND SITE SURFACES
-------------------------------------------------------------------------------

## 7.1 Terrain

Use a 1 m Environment Agency DTM where coverage permits.

Requirements:

- preserve the steeper fall west of the castle;
- preserve the gentler northern slope;
- represent the ha-ha as terrain where supported;
- do not flatten the grounds into one platform;
- prevent isolated one-block spikes and pits;
- document any bounded smoothing;
- do not move walls, roads, or foundations vertically through cosmetic smoothing;
- use local foundation pads only where required and blend them credibly;
- use the canonical terrain-floor resolver for authored placement;
- keep roads and paths on the resolved surface;
- avoid impossible threshold steps;
- preserve 1 m vertical scale.

Use DSM minus DTM cautiously for building and canopy height. Filter vehicles, temporary objects, scaffolding, and vegetation contamination before using a height.

Add a horizon only after playable terrain is complete. Horizon styling may not alter playable geometry or conceal AOI-edge mistakes.

## 7.2 Roads, drives, paths, parking, and boundaries

Inventory every significant route and boundary in the AOI, including:

- Castle Street;
- Church Road;
- Park Road;
- western and eastern castle approaches;
- drives through the outer and inner gatehouses;
- present service and parking access north of the castle;
- the modern kitchen-court wall breach;
- churchyard paths;
- formal garden paths;
- privy-garden gravel paths;
- goodly-garden axial and perimeter paths;
- paved or gravel courts;
- nearby access routes inside the 100 m buffer.

For each route determine centreline, width, shoulder or verge, material, elevation, topology, wall or gate crossings, and access type.

Distinguish at least asphalt, gravel, stone paving, compacted earth, lawn, and parking surface. Do not turn every route into asphalt.

Use cells layers for horizontal surfaces where the package contract fits. Use structures only for vertical furniture, kerbs, walls, gates, steps, retaining elements, and similar geometry.

All intended exterior routes must be traversable with the production player controller.

## 7.3 Hydrology

Perform an explicit hydrology inventory covering waterways, ditches, drains, ponds, natural-water polygons, LiDAR depressions, and historic hypotheses.

Rules:

- model only current, evidentially supported water or drainage;
- do not create a moat;
- do not create the conjectural western canal;
- do not fill the ha-ha with water without current evidence;
- omit the water layer if no permanent surface water exists, and state that as a researched result;
- represent a dry ditch as terrain, not `WATER` blocks.

-------------------------------------------------------------------------------
8. CASTLE COMPLEX
-------------------------------------------------------------------------------

The castle is not a generic footprint extrusion. Author it from explicit ranges, towers, courts, walls, gates, openings, roofs, and ruins.

## 8.1 Inner court

Model:

- west range;
- central gatehouse;
- north range;
- south range;
- open eastern side;
- completed and incomplete tower masses;
- polygonal towers;
- gate passages;
- parapets and battlements;
- principal roof forms and ridge directions;
- lead, stone-slate, and tiled distinctions where supported;
- major red-brick chimney stacks;
- courtyard lawn and circulation;
- major windows and doors;
- south-range double-height compass windows;
- important buttresses, bays, recesses, and silhouette changes.

Do not fill the absent east range. Preserve the current open condition. A buried-range overlay, if implemented, must be development-only, source-backed, and visibly separate.

## 8.2 Outer court

Model its unfinished and ruinous present state:

- north and west ranges at right angles;
- roofless portions;
- central outer gateway;
- square and polygonal towers;
- visible basement or semi-basement openings;
- crossed arrow loops;
- courtyard-facing window and doorway rhythm;
- exposed shell interiors;
- surviving partitions where they shape traversal;
- correct tower and wall heights;
- connection to the inner-court west range;
- current alterations affecting massing;
- approximately 87 m kitchen-court wall extension;
- current car-park access breach.

Do not add intended but never completed floors or roofs.

## 8.3 Garden walls

Model:

- western privy-garden walls;
- lower eastern goodly-garden walls;
- embattled parapets and coping;
- buttressing;
- major doors and high-level openings;
- surviving openings associated with the lost gallery;
- oriel openings in the southern wall;
- visually legible phase junctions, including the documented approximately 18 m junction;
- eastern bee-boles at approximately 1 m height and 4 m spacing;
- south-west connection toward the churchyard boundary.

At 1 m resolution, choose the smallest stable representation of bee-boles, slit windows, crenellations, tracery, and similar details. Do not create glittering voxel confetti to claim completeness.

## 8.4 Architectural representation rules

- Use measured wall centreline and thickness.
- Use supersampled or otherwise tested area-preserving rasterisation for diagonals and polygons.
- Use explicit negative-space masks for gates, doors, windows, arches, and roofless shells.
- Keep arches coherent and traversable.
- Remove floating single blocks around openings.
- Preserve principal façade bay counts and spacing.
- Preserve roof slopes and ridge direction with deliberate stepped voxel roofs.
- Preserve the hierarchy of towers, lower unfinished ranges, parapets, and chimneys.
- Keep visible and collision geometry consistent.
- Do not use invisible decorative blockers.
- Prefer silhouette, opening rhythm, massing, and material hierarchy over unsupported micro-ornament.

-------------------------------------------------------------------------------
9. GARDENS, CHURCH, LODGES, AND 100 M CONTEXT
-------------------------------------------------------------------------------

## 9.1 Gardens and grounds

Gardens are primary architecture, not green filler.

Model and validate:

- outer-court lawn;
- late twentieth-century vineyard west of the outer court;
- Howard family graveyard near West Lodge;
- inner-court lawn;
- open lawn east of the castle;
- five Robinia trees east of the castle;
- eastern conifer and Leyland-cypress screen;
- four nineteenth-century lime trees on the western approach;
- privy garden and octagonal central lawn;
- current central sundial or feature;
- gravel paths and borders at engine-appropriate detail;
- goodly garden;
- two rose-garden compartments;
- substantial crenellated yew hedges;
- east-west axial path and north-south paths;
- Arts and Crafts shelter;
- statue position;
- open eastern lawn;
- tower-like yew framing where currently present;
- major Wellingtonia or sequoia, horse chestnut, sycamore, walnut, and other identifiable specimen trees;
- ha-ha;
- screens, hedges, gates, walls, and boundary transitions.

Vegetation rules:

- landmark trees receive measured position, approximate crown diameter, and height;
- formal hedges receive measured footprints and heights;
- vineyard rows follow current alignment;
- context vegetation may be simplified deterministically;
- do not convert every canopy return into a cube tree;
- avoid procedural biome planting in the measured grounds;
- prevent vegetation from intersecting roofs, walls, paths, and façades;
- preserve important sightlines between castle, gardens, lodges, and church.

## 9.2 West Lodge

Model at landmark fidelity:

- square main plan and cross-wing;
- single storey plus attic;
- three-bay east-facing elevation;
- Tudor-Gothic openings;
- projecting stacks;
- clay-tile roofs;
- attached gateway and pedestrian door;
- embattled gateway piers;
- carriage gate;
- adjoining walls.

## 9.3 East Lodge

Model at landmark fidelity:

- L-plan;
- single storey plus attic;
- south road elevation;
- three-bay composition;
- projecting gable;
- canted corner;
- stone and brick stacks;
- clay-tile roof;
- attached single-storey outbuildings;
- relationship to Park Road and the eastern approach.

## 9.4 Church of St Mary the Virgin

Do not reduce the adjacent Grade I church to a generic village box.

Model at landmark fidelity:

- nave;
- north and south aisles;
- chancel;
- south Stafford chapel;
- two-storey south porch;
- four-stage west tower;
- diagonal buttresses;
- battlements;
- openwork crown and turrets;
- principal roof ridges;
- Cotswold stone-slate roofs;
- major windows and entrances;
- churchyard walls and principal paths;
- spatial relationship with the castle garden wall and West Lodge.

Private or unsupported interiors are outside scope.

## 9.5 Remaining context

Include every significant building footprint, road segment, boundary, and terrain feature intersecting the AOI.

For non-landmark context buildings:

- preserve footprint and orientation;
- estimate eaves and ridge heights from cleaned DSM minus DTM where reliable;
- use current roof form when recoverable;
- simplify façade detail;
- do not invent interiors;
- distinguish masonry, render, brick, and roof families only where supported;
- provide enough massing to make approaches and views geographically recognisable.

The heritage core must not dissolve into a generic procedural suburb.

-------------------------------------------------------------------------------
10. AKIYABLOCKS MATERIALS, STYLE, AND DISTANCE RENDERING
-------------------------------------------------------------------------------

Inspect the current implementation on `prototype/constructive-distance-lod` before selecting a material strategy.

The scene needs a restrained, reusable British historic-material vocabulary capable of distinguishing:

- Cotswold limestone ashlar;
- mixed limestone rubble;
- dressed stone trim;
- pale or pinkish lime-mortar variation where visible;
- Cotswold stone slate;
- clay tile;
- lead roof;
- red brick chimneys;
- timber doors and gates;
- dark window and metal openings;
- gravel;
- stone paving;
- asphalt;
- grass;
- formal dark yew;
- deciduous and conifer foliage.

Do not map a material to `SANDSTONE` merely because both are tan. Material identity, geological character, lighting response, swatch, and scene readability must agree.

## 10.1 Reuse before extension

First test whether existing generic block identities, semantic face styles, painterly profiles, and world-space material functions can express the required vocabulary. Reuse them where they are semantically honest.

If a new material or block family is required, it must:

- be generic rather than named after Thornbury;
- represent a real reusable family such as pale limestone, stone slate, lead roofing, or formal hedge;
- have stable identity independent of colour;
- work through sync and worker meshing;
- receive correct shader routing and LOD behavior;
- have a matching UI swatch;
- work when placed, broken, persisted, reloaded, and remeshed;
- preserve collision, raycasting, mining, and save behavior;
- avoid RGB-signature dispatch;
- avoid a new partition unless measured and justified;
- include engine contract and regression tests;
- be exported through the SDK only when scene authoring genuinely needs it.

## 10.2 Scene-selected style

**A new registered painterly profile is required, not optional.** Verify this on the
branch you check out, but as of the required base, `KNOWN_PAINTERLY_PROFILES`
(`src/world/scenesContract.js`) contains exactly one entry —
`middle-place-cezanne-v3` — and `CHUNK_VISUAL_STYLES` is down to three
(`classic`, `constructive-flow`, `middle-place-cezanne-v3`). Five earlier painterly
generations were deleted from the branch. There is therefore no profile Thornbury can
reuse except Middle Place's, whose palette is precisely the Southwestern adobe and
red-rock colour language section 1.5 forbids inheriting.

Registering a profile is consequently a general engine change and must go through
section 2.3's decision record. It needs, at minimum: a new member of
`CHUNK_VISUAL_STYLES`, a fragment-shader entry point, a `createDefaultPass` arm, and a
`KNOWN_PAINTERLY_PROFILES` entry. Reuse the shared shader-builder seam
(`buildPainterlySmudgeFragmentShader`) and the shared semantic decode rather than
copying a grammar wholesale — copying is exactly how the five deleted generations
accumulated.

The engine already guards the silent-degradation path here: a test asserts that every
`KNOWN_PAINTERLY_PROFILES` entry resolves to a non-null pass from the real factory, so
registering a profile name without a shader behind it fails the suite rather than
rendering classic in silence. Do not weaken that test to land a placeholder.

Use generic descriptor fields and registered profiles, such as the current equivalents of:

    palette
    painterlyProfile
    fogScale
    fogColor
    clouds

A Thornbury profile may contain scene-specific values but must select generic rendering machinery. It may tune:

- limestone and mortar palette;
- value grouping;
- low-frequency stone variation;
- face emphasis;
- roof response;
- formal and informal greens;
- atmospheric haze;
- distance simplification;
- mark scale and strength;
- silhouette emphasis already supported by the engine.

It must not alter geometry, collision, source measurements, persistence, or input.

## 10.3 Style proof before full rollout

Before styling the entire scene, build a small representative proof containing:

- one ashlar wall with window and buttress;
- one rubble or ruined wall;
- one stepped stone-slate or clay-tile roof;
- one red-brick chimney;
- one gravel-to-lawn boundary;
- one formal yew mass;
- a distant tower silhouette.

Capture the proof in classic/default and proposed profile modes at near, middle, and far distances, in motion and stills, on desktop and phone. Evaluate:

- material recognition;
- mark stability in motion;
- target-highlight clarity;
- opening readability;
- AO and sky-visibility behavior;
- moiré and flicker;
- far silhouette;
- draw calls, geometry bytes, shader compilation, and frame cost.

Do not roll out a style whose still image is attractive but whose marks swim, flicker, erase openings, or collapse on phone.

## 10.4 Existing-scene regression

Every general rendering change must be tested against representative existing scenes. Existing scenes must retain their registered profiles, default behavior, block routing, swatches, and performance unless an intentional engine-wide change is separately approved and documented.

-------------------------------------------------------------------------------
11. SCENE PACKAGE, SDK CONSUMPTION, AND REGISTRATION
-------------------------------------------------------------------------------

Use the external scene-package architecture already established by Akiyablocks.

The source and generated scene package belong in `Akiyablocks-Thornbury`, not as hand-authored content inside engine runtime code.

Expected generated package shape, adjusted to the current contract:

    Akiyablocks-Thornbury/dist/scenes/thornbury-castle/
        manifest.json
        terrain.dem.bin.gz
        roads.cells.bin.gz
        structures.bin.gz
        horizon.json.gz        optional
        water.cells.bin.gz     only if supported current water exists
        provenance.json        only if supported by the current package contract

Use:

- DEM for measured terrain;
- cells layers for horizontal roads, paths, and confirmed water where appropriate;
- structures for castle, church, lodges, walls, roofs, vegetation, gates, context buildings, and other 3D content;
- horizon only for sourced distant terrain.

Respect the current structures contract, including:

- absolute world Y;
- no forbidden bedrock writes;
- deterministic canonical ordering;
- no duplicate cells;
- explicit AIR only for intentional carving;
- `IF_AIR` only for soft dressing that must not overwrite authoritative content;
- player edits overlaying authored content in the established order;
- byte-identical output from identical inputs.

The scene repository should declare the engine as its sibling dependency using the current external-scene convention and import only the public SDK entries.

Add a scene-repository command equivalent to:

    npm run bake:thornbury-castle

It must orchestrate deterministic bake and scene-specific validation.

For development, use the documented package overlay mechanism, for example the current equivalent of:

    AKIYA_SCENE_PACKAGE_OVERLAY="thornbury-castle=../Akiyablocks-Thornbury/dist/scenes/thornbury-castle" npm run dev

Do not invent a Thornbury-only Vite middleware or loader.

In `Akiyablocks`, add the smallest current registration descriptor, likely under:

    src/world/registered-games/thornbury-castle.game.js

Expected data includes current equivalents of:

    key: 'thornbury-castle'
    label: 'Thornbury Castle'
    assetBase: 'scenes/thornbury-castle/'
    hidden: false
    compass: 'on'
    biomes: []
    viewDistance: evidence-based value
    palette: registered palette
    painterlyProfile: registered profile
    surface: registered generic rule

Register it through the explicit static descriptor registry. Do not hand-write a parallel scene in `scenes.js`. Do not create a duplicate scene cache or test-only instance.

If a distributable engine build requires copying an external package under `public/scenes`, follow the current documented shipping contract and automate the copy or packaging step with hash verification. Never maintain two hand-edited copies of scene data.

Do not attach unrelated quest runtimes or Middle Place scenario machinery.

-------------------------------------------------------------------------------
12. SPAWN AND PLAYER EXPERIENCE
-------------------------------------------------------------------------------

Choose a spawn that communicates the real site and supports traversal.

Preferred region:

- western approach near West Lodge, facing toward the castle;
- or another documented public-facing approach if evidence makes it clearly better.

The spawn must:

- stand on stable resolved terrain;
- avoid vegetation, walls, roofs, and private interiors;
- face a recognisable route toward the outer court;
- provide production-player clearance;
- work after save reset and clean reload;
- remain valid with optional water disabled;
- support exterior access to outer court, inner gate, gardens, east approach, and church without flying.

Required traversability routes:

1. West approach to West Lodge.
2. West Lodge to outer court.
3. Outer court through the inner gatehouse.
4. Inner court to eastern grounds.
5. Castle exterior to privy garden where current access supports it.
6. Formal garden circulation.
7. Eastern approach to East Lodge and Park Road.
8. Churchyard exterior route.
9. Complete primary exterior loop without softlock.

Respect current walls and gates as physical features. Do not erase boundaries merely to create a frictionless theme park.

-------------------------------------------------------------------------------
13. NUMERICAL, ARCHITECTURAL, AND VISUAL ACCEPTANCE
-------------------------------------------------------------------------------

Generate:

    design-docs/thornbury-castle/BAKE_REPORT.json
    design-docs/thornbury-castle/VALIDATION_REPORT.md

Validation must calculate, not merely assert, the following.

## 13.1 AOI

- official polygon source and date;
- exact 100.0 m vector buffer;
- pre-raster buffer tolerance no greater than 0.01 m;
- raster boundary deviation no greater than 1 block;
- AOI area, perimeter, BNG bounds, world bounds, and chunk bounds;
- no unexplained authored feature outside the AOI.

## 13.2 Coordinates and scale

- all official NGR anchors transformed to world space;
- Grade I and II anchor residual no greater than 1 block after voxelisation;
- pre-voxel world-to-BNG round-trip error no greater than 0.01 m;
- orientation tests for north, south, east, and west;
- horizontal and vertical metric scale reported and tested;
- player eye height, door clearance, stair behavior, and route widths plausible at the chosen scale.

## 13.3 Terrain

- vertical scale exactly 1 block per metre unless a documented generic engine-unit correction is required;
- median DTM quantisation residual no greater than 0.5 m;
- 95th-percentile residual no greater than 1.0 m;
- no unexplained single-cell spikes or pits;
- no clipping at world limits;
- at least 8 blocks of headroom above the tallest occupied cell.

## 13.4 Footprints and heights

For inner court, outer court, church, both lodges, and major garden enclosure:

- footprint IoU at least 0.90 against the selected reference;
- edge deviation no greater than 1 block for A or B geometry;
- no greater than 2 blocks for explicit C geometry;
- principal-axis orientation error no greater than 1 degree;
- courtyard and gate topology preserved.

For heights:

- A or B-quality building and wall heights within 1 block;
- C-quality heights within recorded uncertainty, normally 2 blocks or less;
- western garden walls approximately 4 to 5 blocks, eastern portion approximately 1 block lower;
- separate reported values for church tower, castle towers, roof ridges, parapets, and chimneys;
- no raw DSM height accepted without ground subtraction and contamination review.

Where sources conflict, report each candidate and rationale. Do not weaken criteria silently.

## 13.5 Roads and paths

- centreline deviation no greater than 1.5 blocks;
- width deviation no greater than 1 block;
- complete junction topology;
- routes aligned through gates;
- no road through a wall or building;
- sufficient player clearance on primary routes.

## 13.6 Historic dimensional checks

Report baked values for:

- western approach length;
- 87 m kitchen-court wall extension;
- 13 m connecting portion;
- principal garden-wall heights;
- bee-bole spacing where represented;
- separation and orientation of both lodges;
- church-to-castle relationship.

## 13.7 Determinism

Run the bake twice from the same source lock and cache. Require byte-identical terrain, structures, roads, optional water, and stable manifest content. Record hashes. Keep wall-clock timestamps outside package identity.

## 13.8 Architecture contract checks

Add automated checks proving:

- no scene-repository deep import from engine internals;
- no copied engine format constants or validators where the SDK owns them;
- no `thornbury-castle` branch in generic mesher, shader, world, input, persistence, or lighting modules;
- scene-specific coordinates and heritage feature names remain outside generic engine algorithms;
- any new SDK export is explicit and test-pinned;
- profile and palette names resolve;
- default behavior remains unchanged when the Thornbury profile is inactive;
- there is only one registered runtime scene instance and package cache;
- package verification uses the same shared validators as runtime loading.

## 13.9 Aesthetic acceptance

The style passes only when:

- castle and church silhouettes are recognisable from canonical middle and far views;
- ashlar, rubble, roof, brick, path, lawn, hedge, and tree families remain distinguishable in representative light;
- world-space marks remain fixed to surfaces during strafing and turning;
- target highlights and openings remain clearer than decorative marks;
- no persistent moiré, crawling, LOD shimmer, or high-frequency phone collapse appears;
- far LOD preserves towers, major roofs, enclosing walls, church tower, and landmark trees;
- overcast, daylight, and dusk remain readable rather than becoming one muddy value band;
- existing scenes retain their intended profiles and material routing after generic engine changes.

-------------------------------------------------------------------------------
14. AUTOMATED TESTS AND PRODUCTION PROOFS
-------------------------------------------------------------------------------

Add focused tests for:

- source-lock schema and licences;
- BNG/world projection and inverse;
- exact AOI buffer and clipping;
- unit scale and datum lock;
- LiDAR crop and nodata handling;
- supersampled polygon rasterisation;
- diagonal and polygonal wall preservation;
- arches and opening masks;
- duplicate voxel prevention;
- terrain-floor placement;
- control points and key dimensions;
- required buildings and gardens;
- buried east range absent from normal structures;
- lost gallery absent from normal structures;
- truthful hydrology layer;
- deterministic output;
- manifest and structures contracts;
- package verification;
- descriptor and static discovery;
- palette and painterly-profile registration;
- spawn validity and route clearance;
- world-height bounds;
- no unknown block IDs;
- no scene-key shader routing;
- SDK import-boundary enforcement;
- worker and synchronous meshing parity for any new material identity;
- existing-scene regressions;
- save, reload, reset, edit, remesh, and context restoration where relevant.

Use existing test helpers and shared validators rather than parallel Thornbury-only substitutes.

Run the exact current equivalents of:

Scene repository:

    npm run bake:thornbury-castle
    npm test
    npm run lint
    npm run typecheck

Engine repository:

    npm run verify:scene-package -- ../Akiyablocks-Thornbury/dist/scenes/thornbury-castle
    npm run lint
    npm run typecheck
    npm test
    npm run build

Adapt command syntax to current scripts. Do not report a verifier as passed unless it exercised the Thornbury package.

-------------------------------------------------------------------------------
15. VISUAL VALIDATION
-------------------------------------------------------------------------------

Extend the production visual-capture manifest with fixed Thornbury views. Pin scene, source-lock identity, seed, time, day, position, yaw, pitch, viewport, style profile, and expected purpose.

Required canonical views:

1. West Lodge and gateway from Castle Street.
2. Western approach toward outer court.
3. Outer-court overview.
4. Outer gate and ruined ranges.
5. Inner gatehouse and inner court.
6. South range from privy garden.
7. Compass-window façade.
8. Privy-garden octagonal lawn.
9. Goodly-garden yew compartments.
10. Eastern garden wall and bee-boles.
11. East Lodge and approach.
12. Church and castle relationship.
13. Kitchen-court wall and car-park breach.
14. Broad elevated site overview.
15. View from or toward the 100 m AOI edge.
16. Overcast daylight.
17. Clear daylight.
18. Dusk.
19. Deep shadow or interior-facing gateway proof.
20. Phone portrait.
21. Phone landscape.
22. Representative style-proof wall while strafing.

Use the production capture path. Wait for the engine's real readiness signal. Hide non-canvas diagnostics. Pin time and seed. Do not read pixels directly from a non-preserved canvas.

Review for:

- geospatial orientation;
- landmark silhouette;
- tower and roof proportions;
- court topology;
- garden-wall enclosure;
- church relationship;
- path and gate alignment;
- material hierarchy;
- vegetation occlusion;
- diagonal aliasing;
- flickering crenellations;
- mark swimming or moiré;
- LOD popping;
- target-highlight competition;
- accidental desert or Southwestern vocabulary;
- missing or speculative structures;
- floating geometry;
- terrain seams;
- AOI-edge cuts;
- phone readability.

Capture short fixed motion paths for large walls, roof approach, garden paths, gate transitions, interior-to-exterior light changes, and fast look across skyline. Still frames alone cannot expose crawling marks.

Create:

    design-docs/thornbury-castle/VISUAL_REVIEW.md

For each view record purpose, exact camera, source references, active profile, result, defects, repairs, and residual limitations.

-------------------------------------------------------------------------------
16. PERFORMANCE AND LOD
-------------------------------------------------------------------------------

Measure rather than declare the scene affordable.

Record at desktop and phone presets:

- package bytes by layer and decompressed bytes;
- load and generation time;
- chunk count;
- voxel, road-cell, water-cell, and landmark-vegetation counts;
- geometry bytes;
- draw calls and triangles;
- frame p50 and p95;
- slow-frame share;
- upload or remesh timing where available;
- peak JS heap;
- shader compile or link warnings;
- GPU and browser identity;
- profile and LOD state.

Compare with at least one existing DEM scene and Middle Place under the same procedure.

Performance principles:

- preserve measured geometry first;
- remove invisible fill before deleting visible landmarks;
- use hollow shells where collision and visuals permit;
- use established LOD and constructive-distance systems;
- keep context buildings simpler than castle, church, and lodges;
- express sub-block ornament through stable material and silhouette choices rather than unstable cube noise;
- do not reduce real-world scale to gain speed;
- do not add a permanent fullscreen cost without phone measurement;
- do not hide failure behind excessive fog.

State every material regression quantitatively.

-------------------------------------------------------------------------------
17. IMPLEMENTATION GATES
-------------------------------------------------------------------------------

Proceed sequentially. Each gate requires executable evidence.

## Gate 0: Repository, architecture, source, and style feasibility

Pass only when:

- both base SHAs and baselines are recorded, including the non-zero typecheck baseline;
- two-repository ownership and SDK boundaries are mapped;
- **the required source endpoints are reachable from this environment**, proved by an
  actual request to the Historic England NHLE feature service and to the Environment
  Agency elevation catalogue — not by asserting that the URLs exist. If the environment
  has no outbound network access, or either service is unreachable or has moved, **stop
  and report at Gate 0**. Every later gate depends on this data, and no amount of
  authored geometry substitutes for it. Do not proceed on invented coordinates,
  remembered figures, or a hand-traced boundary;
- required data can be lawfully obtained;
- official grounds polygon and 1 m DTM coverage are confirmed;
- 1 m block scale is proved against player and world constraints, **and the vertical
  budget of section 1.2 is computed in blocks against the branch's `CHUNK_Y`, with a
  stated source for each term, and fits**;
- no blocking licence conflict remains;
- existing Akiyablocks visual devices are inventoried, including the current contents of
  `CHUNK_VISUAL_STYLES` and `KNOWN_PAINTERLY_PROFILES`;
- a style proof plan exists;
- the new painterly profile required by section 10.2 has a decision record;
- the new-material cost of section 10.1 is estimated rather than deferred: semantic
  surface class is driven by hardcoded block-ID tables in the engine's paint-semantics
  module, so each new stone, slate, lead, tile, or hedge identity needs a block ID, an
  entry in those tables, a UI swatch, and worker-and-sync meshing parity. Count them at
  Gate 0; this is the largest engine-side cost in the campaign;
- every proposed engine change has a contract owner and default-inert design.

## Gate 1: Coordinate and terrain substrate

Pass only when:

- source lock exists;
- exact grounds polygon and 100 m buffer exist;
- projection tests pass;
- 1 m terrain is baked;
- vertical scale and datum are stable;
- terrain errors meet thresholds;
- spawn candidate has valid ground;
- package can be read through shared SDK and verifier paths.

## Gate 2: Circulation, boundaries, and context skeleton

Pass only when:

- roads, paths, drives, parking, walls, and hydrology inventory are baked;
- all major footprints appear correctly;
- church and lodge anchors align;
- AOI clipping passes;
- primary route topology exists;
- no engine special case was introduced for basic package loading.

## Gate 3: Castle and garden landmark geometry

Pass only when:

- inner court is recognisable and measured;
- outer court is correctly ruinous;
- gate passages work;
- garden walls and major openings exist;
- buried east range remains absent;
- footprint and height thresholds pass;
- west approach reaches inner court;
- close and middle-distance silhouettes pass initial review.

## Gate 4: Aesthetic system, church, lodges, gardens, and vegetation

Pass only when:

- representative style proof passes motion and phone review;
- any generic engine material work is modular, profile-driven, documented, and regression-tested;
- church and lodges meet landmark criteria;
- formal gardens and structural vegetation exist;
- material hierarchy reads correctly;
- no landmark vegetation intersects architecture;
- existing scenes remain correct.

## Gate 5: Registration, full package, LOD, and performance

Pass only when:

- scene is registered through the generic descriptor path;
- external package overlay loads cleanly;
- deterministic double-bake succeeds;
- production verifier passes;
- targeted and repository-wide tests pass;
- lint and build pass, and typecheck shows no new errors against the Gate 0 baseline
  (see section 3 — the baseline is not zero);
- canonical still and motion captures complete;
- performance report is populated;
- full exterior route completes from clean state;
- save, reload, reset, player edits, and remeshing do not corrupt the scene.

After Gate 5, rerun every gate from clean generated state and exact recorded SHAs. Do not rely on accumulated session state.

-------------------------------------------------------------------------------
18. REQUIRED DELIVERABLES
-------------------------------------------------------------------------------

The campaign must leave:

1. A playable registered `thornbury-castle` scene.
2. A deterministic external scene package in `Akiyablocks-Thornbury`.
3. A reproducible fetch, derive, author, bake, and validation pipeline.
4. Exact 100 m AOI construction.
5. Proven human and metric scale.
6. Castle inner and outer courts at landmark fidelity.
7. Present-day gardens and grounds.
8. Both lodges.
9. St Mary's Church.
10. Roads, drives, paths, parking, boundaries, and researched hydrology.
11. Significant 100 m context.
12. Source lock, licences, and attribution.
13. Measurement ledger and uncertainty log.
14. `AESTHETIC_DIRECTION.md`.
15. `ENGINE_DECISIONS.md`.
16. Automated numeric, architecture, and regression validation.
17. Visual capture definitions, stills, motion proofs, and review.
18. Performance and LOD report.
19. Engine-side reusable changes, if any, modularised and documented according to Akiyablocks contracts.
20. Final implementation report.

Create the final report at:

    design-docs/thornbury-castle/IMPLEMENTATION_REPORT.md

It must include:

- scene and engine base/final SHAs;
- branch names;
- ownership and architecture summary;
- exact AOI area and bounds;
- world origin and transform;
- source inventory, dates, licences, and attribution;
- current versus historical-state decision;
- aesthetic principles and profile choices;
- engine changes, contract rationale, default behavior, and rollback path;
- package sizes and layer counts;
- voxel, road, water, and vegetation counts;
- control-point residuals;
- dimensional, terrain, footprint, and height validation;
- deterministic hashes;
- test, lint, typecheck, build, verifier, and browser results;
- desktop and phone performance;
- capture inventory;
- defects found and repaired;
- remaining C and U uncertainties with player-visible consequence;
- explicit exclusions;
- exact bake and run instructions.

-------------------------------------------------------------------------------
19. DEFINITION OF DONE
-------------------------------------------------------------------------------

This campaign is done only when a player can select Thornbury Castle through the normal Akiyablocks scene path and walk through a metrically credible present-day site whose terrain, castle, gardens, church, lodges, approaches, roads, and 100 m context align with researched geography, while the scene's atmosphere, materials, silhouettes, and distance behavior use Akiyablocks' established constructive visual grammar.

It is not done when:

- only a plan or research dossier exists;
- the castle is a generic extrusion;
- terrain is flat or vertically compressed;
- the site is centred by eye;
- the 100 m extent is a point-radius circle;
- only OpenStreetMap defaults were used;
- church, lodges, or formal gardens are missing;
- lost Tudor buildings appear as current structures;
- a moat or canal was invented;
- routes pass through walls;
- the scene requires flying for ordinary exterior traversal;
- the scene is reachable only through an undocumented special URL;
- the package loader contains a Thornbury special case;
- the scene repository deep-imports engine internals;
- general engine code contains Thornbury geometry or scene-key branches;
- a new renderer or material path bypasses Akiyablocks profiles, blocks, swatches, and lifecycle;
- the style looks attractive only in one still frame;
- screenshots replace numerical validation;
- tests never exercise the package in production runtime;
- existing scenes regress silently;
- phone rendering or navigation fails;
- provenance or licensing is unknown.

-------------------------------------------------------------------------------
20. FINAL CLAUDE CODE RESPONSE
-------------------------------------------------------------------------------

At completion respond with:

1. Concise implementation summary.
2. Both repositories, branches, and exact base/final SHAs.
3. Added and modified files grouped by repository and architectural purpose.
4. Exact AOI, origin, horizontal scale, vertical scale, and world bounds.
5. Principal sources, survey dates, licences, and attribution.
6. Key dimensional, geospatial, terrain, footprint, and height results.
7. Aesthetic direction, profile, material families, and near/middle/far behavior.
8. Every general engine change, its reusable contract, tests, default behavior, and reason it could not remain scene data.
9. Package sizes, counts, and deterministic hashes.
10. All test, lint, typecheck, build, verifier, browser, and capture results.
11. Desktop and phone performance.
12. Canonical still and motion capture paths.
13. Remaining uncertainties with confidence class and player-visible consequence.
14. Exact commands to fetch, bake, verify, run, and capture the scene.

Do not use vague statements such as `looks accurate`, `roughly matches`, `engine-compatible`, or `all tests should pass`. Supply measurements, commands, hashes, captures, and concrete evidence.