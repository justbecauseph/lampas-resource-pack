# Lampas Resource Pack

This repository contains the unified resource pack for the **Lampas** Minecraft server. It is configured to override and customize resources (textures, languages, models, etc.) for various Minecraft mods in a single, consolidated pack.

---

## 📂 Repository Structure

The resource pack is structured in a standard Minecraft format:

```text
lampas-resource-pack/
├── .github/workflows/
│   └── release.yml          # GitHub Actions autoversioning workflow
├── assets/                  # Root folder for all mod resource overrides
│   └── <mod_id>/            # Namespace folder for a specific mod (e.g., lightmanscurrency)
│       ├── lang/            # Localization files (e.g., en_us.json)
│       ├── textures/        # Texture overrides (blocks, items, UI, etc.)
│       └── models/          # 3D block and item models
├── pack.mcmeta              # Resource pack metadata (defines format and description)
└── README.md                # This documentation
```

---

## 🛠️ How to Add or Update Resource Packs

You can target resources for any mod installed on the server by placing them under the correct namespace in the `assets/` folder.

### Step 1: Find the Mod ID
Locate the mod's ID (or namespace). For example:
- Minecraft (Vanilla): `minecraft`
- Lightman's Currency: `lightmanscurrency`
- Iron Chests: `ironchests`

### Step 2: Mirror the Asset Path
To override resources, you must match the exact path used by the original mod.
1. Create a folder inside `assets/` named after the Mod ID (e.g., `assets/ironchests/`).
2. Replicate the target directory structure inside it.
   - **For Renaming Items / Tooltips**: Place translation files in `assets/<mod_id>/lang/en_us.json`.
   - **For Overriding Textures**: Place image files in `assets/<mod_id>/textures/item/` or `assets/<mod_id>/textures/block/`.

### Step 3: Configure Metadata
If you upgrade the Minecraft version of the server, check the `pack_format` in [pack.mcmeta](file:///C:/Users/markj/source/repos/lampas-resource-pack/pack.mcmeta).
* Current format for **1.21.1** is **`34`**.

---

## 🚀 Automatic Releases & Deployment

This repository uses GitHub Actions for **autoversioning** and deployment. Any push to the `main` branch automatically triggers a release.

### Workflow Process
1. **Auto-Increment**: A new tag (`v0.0.<run_number>`) is automatically created.
2. **Packaging**: All files under `assets/`, `pack.mcmeta`, and `pack.png` are bundled into a ZIP archive.
3. **SHA-1 Calculation**: The runner calculates the SHA-1 hash of the ZIP.
4. **Publishing**:
   - Creates a new versioned release on GitHub.
   - Updates the **Latest Release** on GitHub, overwriting the permanent `lampas-resource-pack.zip` asset.

### Server Configuration
In your Minecraft server's `server.properties` file:

```properties
# Always points to the latest compiled version of this pack
resource-pack=https://github.com/justbecauseph/lampas-resource-pack/releases/download/latest/lampas-resource-pack.zip

# Update this with the new SHA-1 hash found on the GitHub Releases page after a push
resource-pack-sha1=<copy-sha1-hash-from-github-release-notes>
```
