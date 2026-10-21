# Review of Lab 02 and teaching recommendations

Reviewed on 19 October 2026. The revised student exercise is [labs/lab_02.md](../labs/lab_02.md). The [original draft](lab_02_original_2026-10-19.md) is preserved unchanged; line references below refer to that copy.

## Overall judgment

Keep the Villach historical-map task. It offers a worthwhile progression from opening and styling existing vector data in Lab 01 to constructing and evaluating spatial reference information. The draft's strongest elements are the local example, emphasis on point distribution, and invitation to consider historical uncertainty.

The original should not be issued unchanged. It risks teaching that a small fitting error proves positional accuracy, that output pixel size sets an accuracy tolerance, and that changing the project CRS fixes a layer's location. Those are conceptual errors, not merely outdated menu instructions. The revision centres the exercise on a question students can answer with evidence: **how well does this transformation locate identifiable features within a defined study area, relative to the chosen reference?**

The repository README allocates 30 minutes to theory and approximately 60 minutes to practical work. The revision therefore uses one required transformation, six controls, three withheld checks, and a short report completed after class. Timing is a planning estimate, not a result from a student pilot. Final classroom release still depends on checking the distributed image and piloting feature matching.

## Priority corrections

| Priority | Evidence in original draft | Diagnosis and revision |
| --- | --- | --- |
| Essential | Lines 79–92: lower RMSE means better accuracy; aim below half a pixel | A fitting statistic is not an independent accuracy test. The proposed 0.25 m threshold is unsupported by historical-map quality, reference accuracy, or point-identification uncertainty. Remove it and assess withheld points in explicit units. |
| Essential | Lines 19–22: image already has a CRS and 0.5 m pixels | Distinguish source-product metadata, the unreferenced teaching copy, and target-output settings. Local evidence shows two different versions; see the data audit below. |
| Essential | Lines 52–54: setting the CRS ensures alignment and accurate measurements | The project CRS controls display coordinates. Correct source CRS descriptions and valid coordinate operations are needed for alignment. Assigning a CRS does not establish an unknown pixel-to-ground transformation. Measurement behaviour also depends on project settings. |
| Essential | Lines 82–83: remove high-error points to lower RMSE | This rewards selective deletion and can remove genuine evidence of distortion. Require inspection of the physical correspondence, a reason for every correction or exclusion, and preservation of geographic coverage. |
| Essential | Lines 79–97: inspect errors before selecting the transformation | Residuals are conditional on a fitted model. Select Polynomial 1, target CRS, and residual units before interpreting them. |
| High | Lines 38–43 and 58: install Georeferencer and OSM Place Search; then use QuickMapServices | For the documented QGIS 3.44 workflow, Georeferencer is available from Layer. The place-search plugin is unused; QuickMapServices is assumed but not installed. Reuse the built-in OSM XYZ connection from Lab 00. |
| High | Lines 58, 66, 70: accurate basemap points and even distribution for maximum accuracy | OSM is a reference with limitations, not ground truth. Spatial coverage helps constrain a fit; it does not guarantee accuracy. Require matching physical geometry, not map labels or symbols, and an explicit study extent. |
| High | Lines 66 and 140: at least five points, then Polynomial 2 or TPS | Polynomial 2 needs at least six suitably arranged controls, so the original minimum cannot support that extension. The algebraic minimum also gives little diagnostic redundancy. Use affine in the core; offer a controlled Helmert comparison. Reserve higher-order models for an instructor demonstration or later exercise. |
| High | Lines 120–128: visually decide whether accuracy is acceptable | Provide a repeatable check: three withheld point pairs, discrepancies in metres, a clearly defined RMS calculation, and a conclusion tied to use and extent. |
| High | Lines 137–141: open-ended independent exploration and short report | The task lacks a bounded comparison, required evidence, and a clear completion standard. Specify the small submission and assess interpretation rather than numerical optimisation. |
| Medium | Lines 101–108: settings without rationale | Affine is a sensible baseline. Cubic is defensible for visual display of a colour scan, so it is not inherently wrong; nearest neighbour is chosen here to simplify the explanation and avoid colour interpolation. Neither choice establishes geometric accuracy. Record output sampling separately. |
| Medium | Lines 131–145: close before saving points; incorrect source credit | Save point data before closing. Replace the copied GeoDa credit with KAGIS attribution, retain uncertainty about sheet dates, and include OSM attribution. The extract's precise provenance and reuse conditions remain to be confirmed. |

The tool corrections and algorithm descriptions were checked against the [QGIS 3.44 Georeferencer manual](https://docs.qgis.org/3.44/en/docs/user_manual/managing_data_source/georeferencer.html). The CRS distinction is supported by the [QGIS projection documentation](https://docs.qgis.org/3.44/en/docs/user_manual/working_with_projections/working_with_projections.html).

## Data audit and implications for teaching

Two local TIFFs were found outside the course repository and inspected without modification. Their first TIFF image directories were read directly, including dimensions, compression, GeoKeys, pixel-scale tags, and tie points. Both have **18,461 × 9,753 pixels and four 8-bit bands**. They are not interchangeable as teaching inputs.

| Local copy | Verified properties | Implication |
| --- | --- | --- |
| `3_Teaching/2_2026_2027/3_lab_assignments/1_lab_data/Franziszeischer_kataster.tif` | 317,191,002 bytes (about 302.5 MiB); LZW compression; no CRS GeoKeys, model pixel-scale, tie-point, or model-transformation tag in the inspected image directory | A candidate unreferenced teaching copy. Absence of these tags is consistent with removal of georeferencing, but does not prove the preparation history or identify the Drive file. |
| `3_Teaching/3_2025_2026/1_402.467/5_exercises/new_order/lab05/class/raw_data/Franziszeischer_kataster.tif` | 720,278,940 bytes (about 686.9 MiB); uncompressed; EPSG:31258; pixel spacing approximately 0.499993 × 0.500016 m; upper-left tie point 485987.2598, 166683.9833 | This copy already carries geographic placement. Its metadata closely matches the original lab description. It is unsuitable as an unexplained blank-scan exercise. |

Paths in this table are relative to `C:/Users/chris/PhD employment/`. The newer folder also contains `Franziszeischer_kataster.tif.points`, with **six enabled point pairs and a target CRS of EPSG:25833**, plus an output TIFF. The saved residual values have no explicit unit declaration in the CSV columns and are not independently validated results. Do not distribute this existing point file unintentionally: it can preload someone else's matches. Do not reinterpret its UTM coordinates as EPSG:31258 coordinates.

A downsampled preview of the older folder's JPEG was inspected. It visibly depicts a broad mosaic around Villach, with sheet boundaries and extensive rural surroundings. At the older TIFF's stated sampling, the extent is approximately **9.23 × 4.88 km**. Searching the full mosaic for unchanged features is a substantial task for novices; it should not consume the whole lab. The preview is contextual evidence, not verification that the newer TIFF or Drive download has identical pixel content.

**Recommended preparation:** retain a clean, unreferenced teaching copy and a separately stored reference product for the instructor. Ideally supply a smaller urban crop that preserves readable building and road geometry, along with an orientation image. Check for embedded georeferencing and external world files or auxiliary metadata. Explain that a teaching copy derived from an already processed mosaic is a reconstruction exercise; removing metadata does not undo earlier rectification or resampling. Do not describe it as a raw historical scan unless its provenance supports that description.

The Drive link could not be retrieved with the web tool, so its contents, access permissions, and equivalence to either local TIFF remain unverified. Exact historical sheet dates, preparation steps, and redistribution conditions also remain unverified. No source rasters or point files were changed.

## What the error statistics mean

For a point with coordinate discrepancies `dx` and `dy`, its total discrepancy is `d = sqrt(dx² + dy²)`. For `n` withheld checks, use `sqrt(sum(d²) / n)`. Report the units, the largest discrepancy, where checks are located, and how features were identified. Avoid implying that three checks characterise every location in a large raster.

There is a QGIS-specific reason to avoid casually calling every displayed number “RMSE.” In the **3.44.0 implementation**, the Georeferencer's `Mean error` uses `sqrt(sum(dx² + dy²) / (n_enabled - minimum_GCP_count))`; the function returns zero at the exact minimum count. For affine, that minimum is three. This is different from the unadjusted RMS discrepancy calculated for withheld checks. Preserve the UI label and units in student reports rather than equating the two. See the [version-specific calculation](https://github.com/qgis/QGIS/blob/final-3_44_0/src/app/georeferencer/qgsgeorefmainwindow.cpp#L1734).

The [3.44.0 GCP implementation](https://github.com/qgis/QGIS/blob/final-3_44_0/src/app/georeferencer/qgsgcplist.cpp#L23) fits using enabled points and updates residuals for both enabled and disabled points. This supports using disabled pairs as checks in the proposed affine exercise. In map units the discrepancy is computed in the target CRS. Pilot the actual classroom build and confirm the table's unit labels; do not generalise this workflow blindly to higher-order transformations.

These are checks of **agreement with the reference**, not independent measurements of absolute ground truth. A common reference bias can remain invisible. If students use a held-out point to tune the fit or choose a model, it has become diagnostic evidence used in model selection; a fresh location is needed for a final independent check.

The 0.5 m sampling claim cannot justify a 0.25 m tolerance. As a scale illustration only, a 0.2 mm marking uncertainty at 1:2880 corresponds to 0.576 m on the ground, before other errors. The exact scale of the supplied extract was not verified, so this is an illustrative calculation, not an accuracy estimate for this map.

## A feasible teaching sequence

Use the preceding theory period to establish image coordinates versus ground coordinates, the idea of a fitted transformation, and the difference between fitting and checking. A sketch with three exact-fitting controls and a misplaced fourth location is more useful at this stage than a catalogue of polynomial models.

| Practical time | Student activity | Instructor action or evidence |
| --- | --- | --- |
| 0–8 min | Set up folders, project, and reference | Confirm everyone has the same image and coordinate-operation configuration. |
| 8–15 min | Open Georeferencer and predict suitable matches | Demonstrate one precise match and one ambiguous or changed feature. Ask students to explain the difference. |
| 15–35 min | Plan roles; enter six controls and three checks | Provide location hints without supplying every coordinate. Check geographic coverage and physical correspondence. |
| 35–45 min | Inspect control residuals and create the raster | Ask for an evidence-based reason before accepting an exclusion. |
| 45–55 min | Examine checks and overlay | Ensure disabled points remain excluded; discuss one discrepancy. |
| 55–60 min | Save points and project; state a provisional conclusion | Ask each student for one supported use and one limitation. Finish calculations and reporting after class if necessary. |

This schedule depends on a manageable study area, predownloaded data, and instructor-tested candidate features. Six controls plus three checks are a teaching compromise, not a universal professional recommendation. If students struggle to find reliable matches, narrow the study area or provide a candidate-feature sheet. Do not trade away the verification step simply to produce a more elaborate map layout.

The required workflow deliberately reuses Lab 00's OSM connection and Lab 01's layer properties. It adds one substantial concept at a time: correspondence, transformation, then checking. Short predictions and explanations replace immediately visible model answers. The optional Helmert comparison changes one modelling choice while holding the inputs constant; Polynomial 2 and TPS would add model-selection and overfitting issues before the core reasoning is secure.

## Suggested assessment and feedback

Treat these as proposed criteria for the instructor, not an announced course grading policy:

| Criterion | Suggested weight | Evidence of success |
| --- | --- | --- |
| Point selection and distribution | 35% | Precise physical correspondences, justified stability, coverage of the stated area, documented corrections. |
| Verification and interpretation | 35% | Checks excluded from fitting, correct units and calculation, interpretation of disagreements, proportionate claims. |
| Reproducibility | 20% | Usable point file, recorded CRS and settings, distinction between project and raster data. |
| Communication | 10% | Legible figures, concise explanation, scale information and source attribution. |

A carefully diagnosed result with sizeable discrepancies can demonstrate more learning than a low-error fit obtained by deleting inconvenient points. If the baseline fit is poor, students should identify plausible causes and limit their conclusions. They should not be forced to claim successful alignment.

Useful discussion answers: changing the project CRS cannot locate unknown pixels; a tiny control residual may coexist with large errors elsewhere; apparent change at a riverbank cannot by itself distinguish historical change from alignment error; finer output sampling adds pixels without adding independent location information.

## Checks before classroom release

1. **Identify the exact distributed image.** Confirm the Drive download, access from a student account, size, unreferenced status, absence of a preloaded point set, and documented origin. Update the student data table if the filename or study extent changes.
2. **Pilot nine plausible correspondences.** Use the same reference students will see. Prepare an orientation screenshot and a short list of candidate features. Verify that feature identity and spatial coverage are achievable; no exact feature pair was certified in this review.
3. **Test the classroom QGIS build.** The revision is documented against 3.44, not executed end to end in QGIS here. Check Georeferencer menus, disabled-point residuals in metres, compression, output sampling, saving and reopening points, and project portability. Set a shared target resolution only if the pilot reveals a practical need, and explain its sampling role.
4. **Standardise the reference and coordinate operation.** EPSG:31258 is retained from the original exercise and is listed by [BEV](https://www.bev.gv.at/dam/bevgvat/PDF-Dateien/Vermessungswesen/Formatbeschreibungen-und-sonstige-Info/EPSG_Austria_BEV.pdf). Confirm that any MGI-to-reference transformation and required grids work on student machines. A supplied reference with documented date, CRS, and quality would support more defensible interpretation than live OSM tiles. An official orthophoto is not automatically free of uncertainty; image date, roof displacement, and feature visibility still matter.
5. **Check practical delivery.** Have an appropriately licensed offline reference available if internet access fails, test on an ordinary student laptop, announce submission details, and confirm historical-source credit and reuse terms with [KAGIS](https://kagis.ktn.gv.at/). Apply [OSM attribution](https://www.openstreetmap.org/copyright) to exported figures.

The broader course also merits a small later correction: Lab 00 describes raster data only as continuous phenomena, although this exercise uses a raster image of discrete cadastral features; its blanket statement that file names are case-sensitive and that periods should be avoided is also too broad. These files were left unchanged because the present task concerns Lab 02.

## Review record

Reviewed the full original Lab 02, Labs 00–01, and the course README; inspected relevant local TIFF metadata and a JPEG overview; checked QGIS documentation and relevant version-specific source code. No student submissions were used. No QGIS desktop run, georeferencing accuracy test, or classroom timing trial was performed.

Original Lab 02 SHA-256: `550C01493AE44E2A8E309EE2F950D02B6F438C3CE620184709DFB1121345D018`.
