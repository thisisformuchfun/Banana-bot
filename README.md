# Garage Banana 01

## Repository recovery status

**Verified on 2026-11-15:** the `main` branch contains only this README. The CAD, simulation, engineering, website, tests, reference images, and license files described below have **not yet been imported into this repository**. The branch list contains only `main`, and there are no open pull requests.

**Do not use GitHub's “Download ZIP” as the project download yet:** it currently contains only this README. The commands below cannot run from this checkout, and the listed local paths are recovery targets, not available files.

The prior README is preserved below as a **historical recovery reference**, not as a verified inventory or validation report. Its dimensions, costs, hashes, simulation results, provenance, licensing statements, and claims of included files have not been independently verified in this documentation correction. Verify them against recovered source files before relying on them. An existing hosted website is separate from this repository; its current contents were not checked in this correction.

## Historical recovery reference (unverified; import pending)

Intended recovery scope: the Garage Banana design, CAD, MuJoCo model and interactive website for **thisisformuchfun/Banana-bot**.

[Live website](https://garage-banana-engineering.stevengineer.chatgpt.site/) · Engineering snapshot (`docs/ENGINEERING_SNAPSHOT.md`, import pending) · CAD assembly (`cad/Garage_Banana_R2_Study.step`, import pending) · Current model (`simulation/banana.xml`, import pending) · BOM (`engineering/bom.json`, import pending)

Approved industrial-design image: `references/approved-id.png` (import pending).

## Start with this robot

**Use `simulation/banana.xml` for the current Garage Banana design.** The runner now defaults to it. `sources/rpo_description/mjcf/rpo.xml` is the original RoboParty reference; select it explicitly only for baseline comparisons. The older robot shown in the website's learning films is a different simulation model.

This import preserves the current design. It does not transfer a trained policy from another banana repository or claim that this robot walks. The included `policy.onnx` is the upstream baseline controller. Current dynamics are a **mass-loading study**: original RoboParty inertias remain, with estimated added shell/neck masses. Replacement dynamics and collision geometry still need identification.

| Current snapshot | Value |
| --- | --- |
| Assembly instances | 453 |
| Default-pose overall height | 1.534 m |
| Driven joints / simulated mass | 25 / 37.700 kg |
| Arm and torso cores | Slotted 20 × 20 mm extrusion |
| Legs | Retained RoboParty reference; separate 4040 study preserved |
| Inset LCD | 1536 × 2048; 3,145,728 pixels |
| Head prints | Yellow crown plus olive / brown / dark-brown AMS stem |
| Delivered planning estimate | $13,745.78 against a $10,000 ceiling |
| Current gait transfer | Falls at 4.961 s and 8.781 s in the two saved tests |

These are engineering-review files, not a fabrication release. See the mechanical audit (`engineering/MECHANICAL_AUDIT.md`, import pending) and simulation notes (`docs/SIMULATION.md`, import pending) for the checked scope and open issues.

## Run the current model

Use Python 3.12 in a virtual environment, from the repository root:

```bash
python -m pip install -r simulation/requirements.txt
python simulation/run.py --duration 10 --vx 0.20 --yaw 0.10 --output simulation/local-run.json
python simulation/view.py --model simulation/banana.xml --duration 10 --vx 0.20 --yaw 0.10
```

The runner is headless; the viewer requires desktop OpenGL. Neither command trains a new policy. For a reference comparison, add `--model sources/rpo_description/mjcf/rpo.xml` and use a separate output filename.

Imported model SHA-256: `7c52343bbfb3703a0656d61e2d976df6b84e3400e5aa70d1b53637ca3fa9e197`. Record a new hash and fresh results whenever the model changes.

## Run the website

```bash
python -m http.server 8000 --directory dist
```

Open `http://localhost:8000`. No frontend build is needed. `dist/` contains the current party styling, assembly animation and recovery controls, CAD meshes, X1C/AMS assets, sound effects, films, telemetry, interactive BOM, bundled dependencies and downloads. Playback videos are included; links to full-resolution originals remain in the site.

Website source snapshot: `1c3cfd15094bfc2e5fa2e2aeab78fba5b2ffe8c9`. The existing Site identity is preserved in `.openai/hosting.json`. GitHub commits do not automatically publish the hosted Site.

## Find the files

| Folder | Contents |
| --- | --- |
| `cad/` | STEP assembly, parametric module builders, individual STEP/STL parts, manifests, AMS 3MFs and historical 4040 study |
| `simulation/` | Current MJCF, upstream ONNX policy, runner, viewer, fixed-base IK, tests and recorded results |
| `engineering/` | Integration/model builders, audits, hardware schedule, BOM, procurement and packaging |
| `sources/` | Pinned RoboParty model, meshes, local STEP dependencies, provenance and licenses |
| `dist/` | Complete buildless website and all published assets |
| `tests/` | Website loading regression checks and local-only fault fixture |
| `docs/` | Design notes and preserved engineering/website snapshots |
| `references/` | Approved industrial-design image |

## Rebuild and check

Delivered geometry is included. Install `engineering/requirements.txt` and follow the ordered rebuild commands in the engineering snapshot (`docs/ENGINEERING_SNAPSHOT.md#cad-and-rebuilding`, import pending), from the repository root. Regeneration changes CAD, manifests and audit hashes; rerun dependent checks. The optional manufacturer-CAD comparison requires a separately obtained STEP supplied with `--vendor-step`.

```bash
python engineering/verify_review.py
python simulation/test_ik.py
node --test tests/asset-loader.test.mjs
```

Fixed-base IK does not prove balance or walking. Historical gait results and film telemetry retain their original model identities. Import provenance (`docs/REPOSITORY_IMPORT.json`, import pending) records this transfer's sources and checks.

## Licensing and attribution

Original character supplied by Stephen Shaffer. RoboParty-derived hardware uses CERN-OHL-W-2.0 (`LICENSE-HARDWARE`, import pending); newly authored software uses MIT (`LICENSE-SOFTWARE`, import pending). Upstream policy, code, browser libraries and printer assets retain their own notices. Read SOURCE_NOTICES.md (`SOURCE_NOTICES.md`, import pending), notices under `sources/`, and website asset provenance. No private credentials or external vendor CAD were added.

