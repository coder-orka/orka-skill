---
name: orka-niulai-image
description: Transform photos, film stills, pets, people, or objects into a cute cow-themed plush 3D image while preserving the original subject, identity cues, species, pose, composition, colors, and key props. For pets and animals, render the entire animal subject—not only its hood or accessories—with short dense plush, soft padding, and sparse doll seams while preserving face, eye color, markings, and silhouette; exclude yarn, knitting, crochet, and woven loops. Replace clearly visible animal ears one-for-one with cow ears so the entire final character has only that single ear pair, never extra hood ears, and add exactly one small hanging bell when the upper chest or under-neck area is visible. Use when the user asks for 牛来风格、可爱牛系风格、动物主体毛绒化、短密绒、毛绒牛头套、萌系牛角、宠物耳朵替换成牛耳、头套不要额外耳朵、胸口挂铃铛、给人物或宠物增加牛系元素、主体不变的牛元素改造，or iterative comparison of a cute bovine-themed image edit. Default to the cute subject-preserving mode; use rough film-frame or ink-poster modes only when explicitly requested.
---

# 可爱牛系图片生成

Use the runtime's image-edit tool for an existing image and its image-generation tool only for a new scene. Treat an existing image as `style-transfer`; keep the original subject recognizable instead of replacing it with a generic cow character.

## Choose the mode

- Default to `niulai-cute-3d`: cute, warm, rounded cow-themed 3D with strong subject preservation.
- Use `niulai-film-rough` only when the user explicitly asks for the rough public-film-frame look.
- Use `niulai-poster-ink` only when the user explicitly asks for the ink-poster look.
- Describe the default result as a cute cow-themed interpretation, not an official film specification.

Read [style-spec.md](references/style-spec.md) before authoring the prompt. Read [evaluation-rubric.md](references/evaluation-rubric.md) before judging an output.

## Prepare inputs

1. Label the edit target as Image 1.
2. Use up to two files from `assets/style-reference/` only for bovine feature cues such as horn, ear, muzzle, and rounded body shapes. Do not copy their stiff expressions or rough rendering into the default cute mode.
3. If Image 1 is wider than about 1600 px, resize a working copy first.
4. Lock the original subject count, identity or species, face, markings, hairstyle, clothing-color roles, pose, action, key props, camera crop, and background layout unless the user asks to change them.
5. Add cow elements on top of the preserved subject. Do not replace the subject with a full cow by default.
6. Determine ear visibility before prompting. Treat an ear as clearly visible when its base, outer outline, and direction are readable. Replace clearly visible pet or animal ears with cow ears; do not create cow ears for ears hidden by hair, clothing, headwear, crop, pose, or another object. Count ears across the complete edited character, including any hood or costume: the replacement cow ears are the only ear pair, and the hood must not add side ears, decorative ears, or a second pair.
7. Determine chest visibility before prompting. When the upper chest or under-neck area is clearly visible, require exactly one small centered bell. Attach it to an existing collar or necklace when possible; otherwise use a narrow soft strap. When the area is hidden or cropped, omit the bell and do not change the crop merely to reveal it.
8. Lock source-specific identity and scene cues explicitly. For a cat portrait, restate the cat face, exact eye color such as blue-green, coat pattern, pose, cow hood when already requested, and the original environment such as a sofa scene.
9. For every pet or animal, apply the plush material to the whole visible subject: head, cheeks, muzzle surround, neck, torso, chest, and visible limbs. Keep eyes, nose, mouth, claws, and other identity-critical features crisp and material-appropriate rather than covering them with fabric.
10. Remove source logos, titles, dates, subtitles, and watermarks from the output.

## Add cow elements by subject type

- **People:** preserve facial identity, hairstyle, clothing, body shape, pose, and expression. Add small rounded horns integrated behind the hairline and optional soft cow ears. When the upper chest is visible, add exactly one small bell centered below the neck, attached to an existing necklace or collar when possible.
- **Pets or animals:** preserve species, face shape, eye color, coat markings, pose, body proportions, and the original ear anchors. Convert the entire visible animal subject to a cohesive stuffed-plush interpretation using short dense pile, softly padded volume, and only a few plausible doll seams along body contours or joint transitions. Preserve markings as plush color regions and keep eyes, nose, mouth, whiskers, and other identity-critical features readable. Do not leave the face or body as ordinary photographic fur while only the hood is plush. When native ears are clearly visible, replace each visible ear one-for-one with a soft rounded cow ear at the same base position, approximate size, and direction; remove the native ear shape completely. The replacement cow ears must also serve as the ear components of any cow hood, so the finished character has exactly one ear pair total. Never place extra ears on the hood's outer sides. When ears are unclear or hidden, do not invent cow ears. Place exactly one pair of small rounded horns behind or between the resulting ear positions. When the upper chest or under-neck area is visible, add exactly one small hanging bell, preferably attached to an existing collar, without covering distinctive chest markings. Add a soft muzzle accent only when it does not erase the original species identity.
- **Objects or mascots:** preserve silhouette, function, colors, and recognizable details. Add horn, ear, hoof, bell, or cow-spot motifs without obscuring the original object.
- Horns are the default required cue unless the user says otherwise. Conditional cow-ear replacement and the conditional chest bell are also required when their source regions are visible. These cues are usually sufficient; avoid extra motifs that overwhelm the subject. Enforce a global ear count: never show native ears, hood ears, decorative ears, or any other ears in addition to the one-for-one replacement cow ears.

## Build the first prompt

Use this structure:

```text
Use case: style-transfer
Asset type: <intended use and aspect>
Input images: Image 1 is the edit target; Images 2-N provide bovine shape cues only.
Primary request: Rebuild Image 1 as a cute cow-themed 3D image while preserving <subject invariants>.
Subject lock: Keep the same subject count, recognizable face or species, eye color, markings, hairstyle or clothing, pose, action, props, camera crop, background layout, and original ear anchor positions.
Cow additions: If Image 1's pet or animal ears have readable bases, outlines, and directions, replace them one-for-one with soft cow ears at the same anchors and remove the original ear shapes; otherwise do not add cow ears. The replacement cow ears are the only ears on the complete character and must also function as the ears of any cow hood; do not add separate ears to either side of the hood. Add exactly two small rounded cream-colored horns behind the resulting ear positions or hairline. If the upper chest or under-neck region is clearly visible, add exactly one small warm-brass or material-compatible bell centered there, hanging naturally from an existing collar or a narrow soft strap. If that region is hidden or cropped, omit the bell and preserve the original framing. Treat these as integrated details; do not replace the subject with a generic cow.
Style/medium: rounded toy-like 3D forms, soft cheeks, friendly expressive eyes; for pets and animals, render the entire visible subject—head, face surround, neck, torso, chest, and limbs—as short dense plush with softly padded volume and only a few restrained doll seams along plausible body contours or joints; preserve eyes, nose, mouth, whiskers, markings, and species identity; clean readable silhouettes, warm diffuse light, gentle shadows, harmonious pastel-accented colors, subtle handcrafted texture.
Constraints: <invariants>; for an animal, the whole visible subject must share the short-dense-plush and soft-filled material treatment, not only clothing or accessories; exactly one ear pair total across the subject and hood; exactly one horn pair; horns must be clearly visible but proportionate; when ear replacement applies, no original ear shapes may remain and no additional hood ears may be introduced; use exactly one physically attached, proportionate bell when the chest is visible and keep it clear of the face and important chest markings; no text, logo, watermark, subtitle, or date.
Avoid: animal face or body left as ordinary photographic fur while only the hood is plush, identity loss, species replacement, full cow transformation, seams crossing eyes/nose/mouth, duplicate native-and-cow ear sets, extra ears on either side of a hood, decorative hood ears, cow ears added to hidden or cropped ears, extra horns, duplicate or floating bells, face-level or oversized bells, reframing only to show a bell, distorted face, giant threatening horns, rough rubber muzzle covering the face, creepy expression, dirty low-resolution textures, yarn strands, knitted stitches, crochet texture, woven loops, braided fibers, excessive seams, photoreal horn grafts, excessive accessories, named-studio imitation.
```

For close portraits, preserve the exact head scale and crop. For full-body images, preserve limb positions before adding hoof-like accents. Do not zoom out merely to show the new cow elements.

## Iterate deliberately

1. Generate one first-pass image.
2. Compare target, bovine reference, and output with `scripts/.venv/bin/python scripts/make_comparison.py` when local paths are available.
3. Score all six rubric dimensions. Continue if the total is below 27/30, any dimension is below 4, or an automatic-fail condition applies.
4. Change one dominant failure per iteration:
   - subject became a generic cow -> restore the original face, species, markings, clothing, and silhouette;
   - horns missing or hidden -> add two small rounded horns behind the ears or hairline without changing the crop;
   - horns too large or threatening -> shorten, round, lighten, and integrate them into the head silhouette;
   - visible native ears remain -> replace them at the same anchors with cow ears and remove the original ear silhouettes;
   - duplicate native and cow ears -> keep only one cow ear at each original visible-ear anchor;
   - hood has extra side or decorative ears -> remove every hood ear that is not the one-for-one replacement at an original visible-ear anchor; keep exactly one ear pair on the entire character;
   - cow ears invented for hidden ears -> remove them and keep only horns or another visible cue;
   - bell missing despite a visible chest -> add exactly one small centered bell below the neck, using the existing collar when present;
   - bell floating or misplaced -> attach it physically to the collar or a narrow soft strap and let it hang with gravity at the upper chest;
   - bell oversized or duplicated -> keep one small bell and preserve the face, coat pattern, clothing, and chest markings;
   - chest hidden or cropped -> omit the bell instead of zooming out, reframing, or inventing unseen anatomy;
   - result is creepy or stiff -> soften cheeks, eyes, mouth, pose, lighting, and color transitions;
   - too many cow cues -> keep horns and remove secondary accessories until the subject reads first;
   - face or species drift -> restate identity markers and remove muzzle changes that obscure them;
   - scene drift -> repeat subject position, action, props, background layout, and camera crop;
   - only the hood is plush -> convert the animal's entire visible head, body, chest, and limbs to the same short-dense-plush and soft-filled treatment while preserving face, eyes, markings, proportions, and pose;
   - animal plush material too rough or fibrous -> use short dense pile, soft padded volume, and only a few clean doll seams along contours or joints; remove yarn strands, knitted stitches, crochet holes, woven loops, and braided fibers;
   - cat portrait identity or setting drift -> restate the cat face, exact eye color, coat pattern, pose, cow hood, and source environment such as the sofa scene;
   - style too rough -> replace dirty stretched textures and muddy light with soft handcrafted surfaces and gentle diffuse light;
   - generic cute 3D with no cow identity -> reinforce horns, apply any visible-ear replacement, and add the required chest bell when its placement area is visible.
5. Re-state all invariants on every edit. Stop only after the threshold passes.

## Deliver

Report:

- final image paths;
- final prompt or prompt template;
- per-image rubric score;
- which iteration changed the result materially;
- built-in image generation as the execution mode.
