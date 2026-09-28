# Coastline — Open City

A GTA-inspired desktop browser prototype with an explorable coastal neighborhood, animated human characters, traffic, driveable cars, building collisions, a minimap, and a three-stop driving route.

## Run

On macOS, double-click `Play.command`, or run `python3 launch.py`. To choose a fixed port, from this folder run:

```sh
python3 -m http.server 8879
```

Then open http://localhost:8879 in Chrome, Safari, or another WebGL-capable browser. The game requires HTTP serving; opening index.html directly will not load the model and JavaScript modules.

## Controls

- W / Up: forward; pressing W while reversing stops reverse motion first
- S / Down: brake, then reverse
- A / D or Left / Right: steer
- Shift: sprint / boost
- E: enter a nearby parked car / exit when stopped
- Mouse drag: rotate camera
- C: close / wide camera and recenter behind the car
- H: choose Remy, James, Sophie, Nova, or AX-7 at any time
- B / Bike button: jump onto the orange motorcycle; E dismounts
- Swimming: walk through the seawall opening at Ocean Drive / z=0 and down the beach. WASD to swim; walk back up the slope to leave the water.
- Space: handbrake
- R: reset to the waterfront
- Escape / ?: pause and controls
- ◐: sunset / daylight

An original small prototype, not the actual GTA 6. The people use a textured, animated human model with realistic proportions; the city architecture is procedural. Choose between five characters (Remy, James, Sophie, Nova, AX-7). The crowd mixes human characters, with clothing tint and height variations. Procedural limb animation uses leg IK, and pedestrians turn before changing direction. Trees, lamps, benches, buildings, and parked vehicles block player movement; vehicle collision uses rotated outlines taken from the visible car body, with short movement steps to prevent tunnelling. Traffic brakes for other vehicles. Includes furnished interiors, homes, shops, transport jobs, flights and locally saved wallet/home choices. No combat or full story campaign. Desktop keyboard required.

## Attribution

- Three.js r170, MIT license: https://github.com/mrdoob/three.js
- Remy, James, and Sophie human models: Mixamo model distributed in the [Mixamo character dataset](https://huggingface.co/datasets/Linzhan/Mixamo-Animations-Characters). Procedural idle/walk/run motion is authored in this prototype. Review original asset terms before redistribution or commercial use.
- Ferrari model: Three.js example asset, model by [vicent091036](https://sketchfab.com/models/57bf6cc56931426e87494f554df1dab6). Source: https://github.com/mrdoob/three.js/tree/r170/examples/models/gltf .
- Reflection environment: Venice Sunset HDR from the Three.js example assets (Poly Haven).
- City geometry, UI, building textures, and gameplay created for this prototype.

## Verification

Browser smoke checks passed for asset loading, starting the game, walking, entering a vehicle, driving movement, exiting, pausing/resuming, daylight switching, route activation, all three character choices, mixed crowd identities, detailed vehicle meshes, tree/lamp/bench/parked-car collision, fast movement against a tree, and pedestrian direction changes. Append `?verify=1` to the local URL to rerun these checks. The full three-stop route and every possible collision were not exhaustively tested.

## Driving direction fix

The visual front axle defines vehicle forward. The chase camera recenters behind the car when mouse dragging stops. The HUD shows D / FORWARD, R / REVERSE with a signed speed, or N / STOPPED. Speed reflects actual movement, including zero when an obstacle blocks the car. Append `?directioncheck=1` to run the driving-direction regression checks.

## Open world, bikes, and water

The city generates new districts as you travel north, south, or east. The coastline and ocean continue as you travel, with no outer walls or invisible map limit. Nearby 120-metre districts stream in and distant districts unload to keep memory bounded. District layouts regenerate consistently when revisited; this is a procedural prototype, so architecture repeats. Wallet, home selection and energy are saved in this browser; world objects reset on reload.

Walk through the seawall opening into the water to swim. Vehicles driven into deep water are recovered to the waterfront and the player continues swimming. Two procedural motorcycles use the same driving controls, with narrower collisions and a seated visible rider.

Append `?trafficcheck=1` to test side-by-side and angled car clearance, actual body overlap, following and crossing traffic, district generation out to 3.6 km, bounded chunk retention, and the absence of outer barriers. Append `?expansioncheck=1` to check bikes and swimming. Driving camera position follows the vehicle without trailing drift; the road arrow marks its forward direction.

## Animation correction (v6)

The walking cycle now moves the planted foot backward relative to the advancing body and lifts the foot during its forward return. This removes the reversed stride that made characters look like they were moonwalking. Wheel rotation is derived from the vehicle's actual forward direction and each wheel's measured radius.

`?animationcheck=1` verifies planted-foot stability for all three characters, forward wheel rotation for cars and bikes, and the car's forward axis against its visible tail lights and cockpit. The driving-direction checks also cover forward, reverse, camera position, and backing away from an obstruction.

## Airport and country travel (v7)

Click **✈ Airport** to mark the nearest terminal on the minimap. The home airport is east of the original city, at the end of the eastbound road (x=300, z=20). Park and walk through the terminal entrance, then press **E** to open Departures. Choose India, Japan, France, the United Arab Emirates, the United States, or the United Kingdom. A short flight transition takes you to a separate procedural district with its own airport and a parked rental car. Select Coastline to return to the original city; nothing in the home city is removed.

Destinations are fictional, country-inspired districts with different building palettes, not geographic recreations. Aircraft are scenery, not pilotable. Use `?airportcheck=1` for terminal access, every destination, safe arrivals, and return-flight checks.

## Buildings and homes (v8)

Walk up to a tan entrance door on a city building and press **E** to enter a furnished apartment interior. Explore the living room, bedroom, kitchen and dining area with WASD. Furniture and walls block movement. Press **E** near the entry door, or click **Exit building**, to return to the same street. City buildings use a shared interior layout with different home palettes; these are separate interior spaces, not every floor of the external tower.

Click **⌂ Homes** to select Palm Courtyard, City Loft, or Skyline Residence and move in. Your home selection persists in this browser's local storage. **Go to my home** returns you there. The city, airport, country travel, vehicles, and swimming remain available outside. `?homecheck=1` tests all three homes, indoor movement, furniture and wall collision, exterior return positions, and ordinary building entry.

## Shops, transport jobs, crowds and airport screening (v9)

**City & Jobs** marks shops, bus stations, railway stations, or airport work desks on the minimap. Walk to a marker and press E. Shops are on the north-facing side of buildings; the opposite entrances still open residences. Inside a shop, approach the cashier counter and press E to buy snacks ($12) or water ($6). Supplies restore energy spent working. Your wallet, energy, and inventory are saved in this browser.

Bus, railway, and airport shifts pay $60, $90, and $120 after three marked tasks completed on foot. Press E at each task; jobs cannot be completed remotely and each completed shift pays once. Repeat shifts to earn more. A shift costs 10 energy. Bus stations offer a $5 trip to the local airport; railway stations offer a $15 trip to the next fictional destination district. Stations include shelters/platforms, parked buses or trains, staff and crowds. Transport uses location transitions; buses and trains are not player-driveable.

Flights now require a selected destination, baggage check-in at the labelled counter, security screening at the scanner, and then boarding at Departures. Check-in and screening actions only work when you stand near the correct location. Each new flight needs a fresh boarding pass.

Destination pedestrians now respawn among several checked positions around the player, including on arrival in India. Traffic has visible seated human drivers, and the selected player character is visible in the driver's seat. Unoccupied parked cars remain empty.

`?servicescheck=1` verifies shift payouts, prevention of duplicate or remote payouts, shop purchases, insufficient funds, energy recovery, crowds in India, driver models, and the complete check-in/security/boarding sequence.

## Sleeping and Nova (v10)

Choose a home in **Homes**, enter it, and walk beside the bed in the right-hand bedroom. Press **E**, or click **Sleep until morning** when beside the bed. Your character lies down, the game pauses briefly, and you wake beside the bed at **07:00** with **100 energy**. Sleeping works only in your selected home. The day count is saved locally.

Choose **Nova** with **H** or the character menu. Nova is a customized human character based on the Sophie asset, with a violet outfit, headphones and a courier bag. Her courier perk gives **15% faster sprinting** and **20% more pay** on shifts started as Nova. Existing characters remain available.

`?restcheck=1` checks bed ownership/proximity, sleep and wake positions, full energy recovery, next-morning time, protection against duplicate sleep actions, the new character, and the courier pay bonus.

The interior camera checks the path between the character and camera. In tight spaces it switches to a labelled first-person view so bedroom walls do not block the view.

## Robotic suit (v11)

Press **H** and choose **AX-7** to wear a graphite and metallic robotic suit with a cyan visor and chest reactor. Armor is attached to the human skeleton, so shoulders, arms, legs and boots move with the character. The other four characters and all city features remain available.

`?robotcheck=1` verifies all five choices, AX-7 selection, bone-attached armor and animated transforms.

## GitHub updates

Public repository: https://github.com/indrajeetllmai/coastline-city

This repository contains the complete static game, including its local model assets and Three.js dependencies. Future game changes should be verified, committed and published to this repository as part of the same update. GitHub Pages, when enabled for `main` at the repository root, redeploys after each published update. Local browser saves are not uploaded.
