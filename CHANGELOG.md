# Changelog

## 1.0.0 - 2026-11-25

- Initial release of the Pinlyx Live Chat tag template.
- Loads the live chat widget from `https://api.pinlyx.com/js/widget.js` with your widget ID.
- Optional Live Visitors analytics (`cs.js`) with its own site ID.
- Widget and site IDs are validated (UUID format) before anything is loaded.
- `inject_script` permission limited to `https://api.pinlyx.com/js/*`.
