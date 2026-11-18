<div align="center">

<img src="readme-assets/banner.svg" alt="Retro Mod Pod: a game goes into the Game Pod, a mod into the Mod Pod, the big red KABOOMY button produces a patched ZIP and receipt, and a mismatch produces NO KABOOMY instead" width="100%">

</div>

# Retro Mod Pod

**Feed it a game. Feed it a mod. Press the irresponsible button.**

Retro Mod Pod is a single-file, local browser tool for applying supported retro-game patches without making the user learn the patching ritual first.

Give the **GAME POD** your own game file or game ZIP. Give the **MOD POD** a patch file or mod ZIP. Press **KABOOMY**.

The original input stays untouched. Retro Mod Pod creates a new `__MODDED.zip` and includes a patch receipt showing what it did.

Created by Wakka through directing, testing, and iterating with AI.

**Current release:** v0.1.0  
**Operation:** local / offline  
**License:** MIT

<br>

<img src="readme-assets/hdr-why.svg" alt="Why this exists, origin story. I didn't know how ROM patching worked, so I made it the tool's problem." width="100%">

I made Retro Mod Pod because I didn't know how ROM patching worked.

I kept running into patch formats, base-game revisions, checksums, different patchers, and instructions that assumed I already knew which file mattered and what tool I was supposed to use.

I wasn't trying to become a ROM-patching expert. I knew what I wanted:

**game in one side → mod in the other → KABOOMY → patched game out**

So I made the knowledge part the tool's problem.

Retro Mod Pod tries to identify the patch, identify the correct game payload, verify what it can, apply the patch locally, preserve the original, and package the result. If the situation is ambiguous or the base game does not match what the patch expects, it refuses to guess.

That refusal is part of the design.

<br>

<img src="readme-assets/hdr-start.svg" alt="Quick start, no install. Game in, mod in, press KABOOMY. Nothing is uploaded." width="100%">

<img src="readme-assets/flow.svg" alt="Game pod and mod pod feed the KABOOMY button, which outputs a patched ZIP with a receipt" width="100%">

1. Download `Retro-Mod-Pod-v0.1.0.html` from Releases.
2. Open it in a modern browser.
3. Put your own game file or game ZIP into **GAME POD**.
4. Put your patch file or mod ZIP into **MOD POD**.
5. Press **KABOOMY**.
6. If verification succeeds, Retro Mod Pod downloads a new `__MODDED.zip`.

Nothing needs to be installed and Retro Mod Pod does not upload your game or patch files.

<br>

<img src="readme-assets/hdr-does.svg" alt="What v0.1.0 does, 4 formats applied. Four patch formats applied, verified wherever the format allows." width="100%">

<img src="readme-assets/formats.svg" alt="Patch formats: IPS, BPS, UPS and PPF1/2/3 are applied; xdelta/VCDIFF is detected but not applied; APS, RUP, MOD, BDF and BSPATCH are recognized only" width="100%">

| Capability | Status |
| --- | --- |
| IPS patching | ✅ Supported |
| BPS patching | ✅ Supported |
| UPS patching | ✅ Supported |
| PPF1 / PPF2 / PPF3 patching | ✅ Supported |
| xdelta / VCDIFF | 🟡 Detected, not applied yet |
| APS / RUP / MOD / BDF / BSPATCH | ⚪ Recognized, not applied yet |
| ZIP game packages | ✅ Supported |
| Raw game / ROM / disc-image input | ✅ Supported |
| BPS / UPS source revision checking | ✅ Source size + CRC32 |
| BPS / UPS patch and output validation | ✅ CRC32 checked |
| PPF2 / PPF3 validation data | ✅ Used when present |
| CUE/BIN targeting | ✅ Uses the BINARY image referenced by a single CUE sheet |
| Ambiguous multi-patch packages | ⛔ Refused |
| Ambiguous game targets | ⛔ Refused |
| Original input modification | 🔒 Never |
| Patch receipt | ✅ Included in every successful output |

Common game-image extensions recognized by the v0.1.0 target selector include:

`bin`, `iso`, `img`, `gba`, `gb`, `gbc`, `sfc`, `smc`, `nes`, `n64`, `z64`, `v64`, `nds`, `md`, `gen`, `32x`, `pce`, `rom`, and `chd`.

<br>

<img src="readme-assets/hdr-nokaboomy.svg" alt="NO KABOOMY, refuses to guess. Ambiguous or mismatched? It stops instead of improvising." width="100%">

Retro Mod Pod intentionally stops instead of improvising when it cannot establish a safe target.

Examples include:

- the mod package contains more than one patch
- the game package contains multiple plausible targets
- a BPS or UPS patch expects a different source CRC32
- a PPF validation block does not match
- the patch format is recognized but not implemented in v0.1.0

One of the first real-world tests used the Pokémon Unbound patch. A FireRed file had the expected size but the wrong CRC32, so Retro Mod Pod returned **NO KABOOMY** instead of producing a questionable patched ROM.

That is exactly the behavior I wanted.

<br>

<img src="readme-assets/hdr-receipt.svg" alt="Patch receipt, every output. Every successful ZIP carries RETRO_MOD_POD_RECEIPT.txt." width="100%">

Every successful output contains:

`RETRO_MOD_POD_RECEIPT.txt`

<img src="readme-assets/receipt.svg" alt="A thermal-paper receipt listing what every successful output records: version, input names, patched payload, target selection, patch format, source and patched checksums, and that the original was not modified" width="100%">

The receipt records:

- Retro Mod Pod version
- original game input name
- patched payload
- how the target was selected
- mod input and patch file
- patch format
- source CRC32 and SHA-256
- patched CRC32 and SHA-256
- confirmation that the original input was not modified

<br>

<img src="readme-assets/hdr-local.svg" alt="Local by design, offline. One HTML file. No downloads, no uploads." width="100%">

Retro Mod Pod v0.1.0 is one HTML file containing its interface and patch engine.

It does not download games, ROMs, BIOS files, patches, or mods. It does not upload your inputs to a server.

Use files you are legally permitted to use. Retro Mod Pod itself contains no commercial game data or third-party patches.

<br>

<img src="readme-assets/hdr-limits.svg" alt="Current limits, conservative. xdelta is detected, not applied. Multi-patch mods are refused." width="100%">

v0.1.0 is deliberately conservative.

- xdelta / VCDIFF is detected but not applied.
- Other recognized formats such as APS and RUP are not implemented yet.
- A mod package containing multiple patch files is rejected rather than having the tool invent an order.
- When a patch format does not provide strong source-validation data, target selection necessarily falls back to CUE/package structure and recognized game-image candidates.

<br>

<img src="readme-assets/hdr-contents.svg" alt="Repository contents, 5 files. The tool, the docs, the license, and the release notes." width="100%">

- `Retro-Mod-Pod-v0.1.0.html` — the complete v0.1.0 tool
- `README.md` — project overview and usage
- `LICENSE` — MIT license
- `RELEASE_NOTES_v0.1.0.md` — first public release notes
- `GITHUB_SETUP.txt` — repository About text, topics, and release metadata

<br>

<img src="readme-assets/hdr-license.svg" alt="License, MIT. Original code only. Games, patches and ROMs belong to their owners." width="100%">

Retro Mod Pod's original code is released under the MIT License.

Game names, patches, ROMs, disc images, and other third-party material remain the property of their respective owners. Retro Mod Pod is an independent utility and is not affiliated with game publishers, console manufacturers, ROM-hack authors, or patch-format creators.

<img src="readme-assets/footer.svg" alt="Press the irresponsible button." width="100%">
