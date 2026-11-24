# Pinlyx Live Chat for Google Tag Manager

A Google Tag Manager custom tag template that installs the [Pinlyx](https://pinlyx.com) live chat widget on your site. Paste your widget ID, fire the tag on All Pages, publish. No code edits on the site.

## What it does

- Loads `https://api.pinlyx.com/js/widget.js?id=<WIDGET_ID>`, the same loader as the plain script snippet in Pinlyx.
- Optionally also loads Pinlyx Live Visitors analytics, `https://api.pinlyx.com/js/cs.js?id=<SITE_ID>`. That script has its own site ID, which is not the widget ID.
- Checks that the IDs look like Pinlyx IDs (UUIDs) before loading anything, and fails the tag cleanly if they do not.
- Requests each script once per page, even if the tag fires more than once.
- Asks for one permission only: `inject_script`, limited to `https://api.pinlyx.com/js/*`. A `logging` permission (debug mode only) is used for validation messages.

## Install from the Community Template Gallery

1. In Tag Manager open **Templates**, then **Search Gallery** under Tag Templates.
2. Search for "Pinlyx Live Chat" and click **Add to workspace**.
3. Go to **Tags**, **New**, choose **Pinlyx Live Chat** as the tag type.
4. Paste your **Widget ID** (Pinlyx, Live Chat, the install snippet, the value after `widget.js?id=`).
5. Set the trigger to **All Pages** (or the pages where the chat should show).
6. Save, test in **Preview**, then **Submit** and publish.

## Test it before the gallery (Import)

You can try the template in your own container without waiting for the gallery:

1. Download `template.tpl` from this repository.
2. In Tag Manager open **Templates**, under Tag Templates click **New**.
3. Open the three dot menu in the top right, choose **Import**, and select `template.tpl`.
4. Open the **Tests** tab and click **Run Tests**. All scenarios should pass.
5. Click **Save**, then create a tag from it as described above.
6. Click **Preview**, open your site, and check in the Tag Assistant panel that the tag fired with status **Succeeded**. The chat bubble should appear on the page.
7. In the browser Network tab you should see one request to `api.pinlyx.com/js/widget.js?id=...`, followed by `widget-core.js` loaded by that loader.

The Tests tab does not run field validation. To check it, open the tag, type an invalid ID, and the field shows an error.

## Fields

| Field | Required | Notes |
|---|---|---|
| Widget ID | yes | UUID, 36 characters, for example `123e4567-e89b-12d3-a456-426614174000`. Spaces around it are removed. |
| Also load Pinlyx Live Visitors analytics | no | Off by default. |
| Live Visitors site ID | when the box is checked | A separate UUID from Pinlyx Live Visitors. |

## Notes and limits

- **Consent.** The template does not read consent state itself. If you need consent before the chat loads, use Tag Manager's built in consent settings on the tag (Advanced Settings, Consent Settings), or fire the tag only from a trigger that waits for consent.
- **Content Security Policy.** If your site sets a CSP, allow `https://api.pinlyx.com` in `script-src` and `connect-src`. The loader fetches the widget core and its settings from that host.
- **Install check in Pinlyx.** The "Verify" button in Pinlyx looks for your widget ID in the raw HTML of your homepage. With Tag Manager the ID lives in the container, not in the page source, so that check may not find it even though the widget works. Test on the live site instead.
- **Single page apps.** The tag loads once per page load. Fire it on All Pages or on the initialization trigger, not on every history change.

## For maintainers: publishing to the gallery

The gallery reads this repository as it is, so the files below must stay at the root of the `main` branch: `template.tpl`, `metadata.yaml`, `LICENSE`.

1. Push the repository to GitHub and enable **Issues** (the gallery requires it).
2. In `metadata.yaml` fill in `sha` with the full commit SHA that contains the `template.tpl` you want to publish. The `sha` of the first version can only be known after the first push, so it is empty in the initial commit. Commit that change, and make sure the SHA you list is a commit that already exists on `main`.
3. Open the template in the Template Editor once, tick **Agree to the Community Template Gallery Terms of Service** on the Info tab, and export it again if the editor changes the file.
4. At [tagmanager.google.com/gallery](https://tagmanager.google.com/gallery) choose **Submit Template** and enter the repository URL.
5. For later releases add a new entry at the top of `versions` (newest first) with the new `sha` and `changeNotes`. Updates usually show up in the gallery within two to three days.

## Contributing

Issues and pull requests are welcome. Please keep `template.tpl` importable (open it in a Tag Manager container and run the tests) and add a test scenario for any behavior change.

## License

Apache License 2.0, see `LICENSE`.

Built and maintained by [Pinlyx](https://pinlyx.com/?utm_source=github&utm_medium=readme&utm_campaign=gtm-pinlyx-live-chat), the omnichannel inbox and live chat for Telegram, WhatsApp, Instagram, Messenger, X and email.
