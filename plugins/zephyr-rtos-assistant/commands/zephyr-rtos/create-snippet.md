---
name: "Create Zephyr Snippet"
description: "Create a Zephyr build snippet (YAML + optional devicetree overlay and Kconfig fragment) from snippet name and content. Follows Zephyr Writing Snippets docs."
---
# Create Zephyr Snippet

## Overview
Create a Zephyr build snippet (YAML + optional devicetree overlay and Kconfig fragment) from the provided snippet name and content. If devicetree (DTS) or `.conf` content is not provided, ask the user for it before creating files. Follow [Zephyr Writing Snippets](https://docs.zephyrproject.org/latest/build/snippets/writing.html) and use the in-tree `nus-console` snippet as structural reference.

## Prerequisites and input

- **Snippet name**: Required. Must be valid for use as a directory and YAML `name` (use kebab-case, e.g. `my-feature`).
- **Target location**: Determined by `snippet_root` setting in `zephyr/module.yml`. **Default behavior:** read `zephyr/module.yml` and use the `settings.snippet_root` path (e.g. if `snippet_root: .`, snippets go in `snippets/<snippet-name>/` at project root). User may override with a different path if needed.
- **Devicetree overlay content**: Optional. If not provided, ask: *"Please provide the devicetree overlay content for this snippet (or say 'none' if no overlay is needed)."*
- **Kconfig / .conf content**: Optional. If not provided, ask: *"Please provide the Kconfig fragment (.conf) content for this snippet (or say 'none' if no .conf is needed)."*

Do not create files until you have the snippet name, target location, and at least one of overlay or .conf (or explicit "none" for both).

## Steps

1. **Gather inputs**
   - Read any snippet name, target path, overlay content, or .conf content from the user message (e.g. after `/create-zephyr-snippet`).
   - If overlay content is missing: ask the user for the devicetree overlay content (or "none").
   - If .conf content is missing: ask the user for the Kconfig fragment content (or "none").
   - Normalize snippet name to kebab-case. Use this for the directory name and for `snippet.yml` `name`.

2. **Choose target directory**
   - Read `zephyr/module.yml` and locate `settings.snippet_root` value (e.g. `.` means project root).
   - If the user did not specify a target, use the `snippet_root` path from `module.yml` and create `<snippet_root>/snippets/<snippet-name>/`.
   - For example, if `snippet_root: .`, create `snippets/<snippet-name>/` at project root.
   - Ensure `snippets/` exists under the chosen target; create it if necessary.

3. **Create `snippet.yml`**
   - Create `<snippet-dir>/snippet.yml` with:
     - `name: <snippet-name>` (kebab-case, same as directory).
     - Under `append:`, add only the keys that apply:
       - If overlay exists: `EXTRA_DTC_OVERLAY_FILE: <snippet-name>.overlay`
       - If .conf exists: `EXTRA_CONF_FILE: <snippet-name>.conf`
   - Paths in `snippet.yml` are relative to the directory containing `snippet.yml`. Do not add board-specific or sysbuild sections unless the user requests them.

4. **Create devicetree overlay (if not "none")**
   - Create `<snippet-dir>/<snippet-name>.overlay`.
   - Apply license per `rules/project/license-header.mdc`.
   - Apply namespacing: use `snippet_<name>` or `snippet-<name>` for node labels/names (e.g. for `foo-bar`, use `snippet_foo_bar_dev` or `snippet_foo_bar_dev`). See Zephyr docs "Namespacing".
   - Write valid DTS overlay content as provided or refined from user input.

5. **Create .conf file (if not "none")**
   - Create `<snippet-dir>/<snippet-name>.conf`.
   - Add one Kconfig option per line (e.g. `CONFIG_XYZ=y`). No SPDX in .conf. Use the content provided or refined from user input.

6. **Optional README**
   - Do not add a README unless the user explicitly asks. If they do, add a short `<snippet-dir>/README.rst` or `README.md` with snippet name, usage (e.g. `west build -S <snippet-name> [...]`), and what the snippet does.

## Snippet layout reference

Minimal (conf only):

- `snippets/<snippet-name>/snippet.yml`
- `snippets/<snippet-name>/<snippet-name>.conf`

With overlay:

- `snippets/<snippet-name>/snippet.yml`
- `snippets/<snippet-name>/<snippet-name>.overlay`
- `snippets/<snippet-name>/<snippet-name>.conf` (optional)

Example `snippet.yml` (overlay + conf):

```yaml
name: my-snippet
append:
  EXTRA_DTC_OVERLAY_FILE: my-snippet.overlay
  EXTRA_CONF_FILE: my-snippet.conf
```

## Checklist

- [ ] Snippet name is kebab-case and used consistently for directory and `name` in `snippet.yml`.
- [ ] `snippet.yml` exists and only references existing overlay and/or .conf files.
- [ ] Overlay (if any) has license header per license-header.mdc and snippet namespacing for labels/nodes.
- [ ] .conf (if any) contains valid Kconfig options.
- [ ] All paths in `snippet.yml` are relative to the snippet directory.
- [ ] User was prompted for overlay and .conf content when not provided.

## Notes

- **Default location:** Snippets are created under `<snippet_root>/snippets/<snippet-name>/` where `<snippet_root>` is read from `zephyr/module.yml` `settings.snippet_root` (typically `.` for project root).
- Snippets are automatically discovered from modules that set `snippet_root` in `module.yml` (no need to manually set `SNIPPET_ROOT` CMake variable).
- Apply snippets with: `west build -S <snippet-name> [...]` or `-DSNIPPET="<snippet-name>"`.
- For board-specific overlays or sysbuild `.conf`, extend `snippet.yml` with `boards:` or `SB_EXTRA_CONF_FILE` only if the user requests it.
