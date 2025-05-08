# Extendable Markdown Preview

[Communicating between an extension and a markdown preview script is out of scope.](https://github.com/microsoft/vscode/issues/174080)

This Git branch repurposes the **Markdown Language Features** extension:

- The extension is renamed to **Extendable Markdown Preview** (`nesk.extendable-markdown-preview`).
- Its goal is only to provide an alternative markdown preview, thus:
	- only the preview is built into the extension package ;
	- the custom editor is renamed ;
	- telemetry is disabled ;
	- the `markdown` contribution points are prefixed by `nesk.` ;
	- and the only command left is `nesk.markdown.showPreview`.

## New features

The following new features are available via the exposed API.

The preview script can:
- read settings values in the `<meta id="nesk-markdown-preview-data">` element, based on the `nesk.markdown.additionalSettings` contribution point;
- listen to messages from the extension host with `window.vscode.onDidReceiveMessage`;
- and can send messages to the extension host with `window.vscode.postMessage`.

The extension host can:
- listen to messages from all previews with `api.onDidReceiveMessage`, receiving the preview ID as the second parameter;
- and can send messages to a specific preview with `api.postMessage`, accepting the preview ID as the first parameter.

## Development

Open the repository at its root inside a Dev Container and install the dependencies by running `npm install`.

**Do NOT use the suggested volume inside the Dev Container.**

To test manually, run the **Extendable Markdown Preview** debug configuration.

To build a new version of the extension: `cd extensions/markdown-language-features; npm run package`
