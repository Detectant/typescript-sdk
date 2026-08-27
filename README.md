# [Detectant - Malware Scanning API for TypeScript](https://www.detectant.com)

<p align="center">
  <img src="https://www.detectant.com/images/detectant-github-banner.png" alt="Detectant" width="100%">
</p>

# Detectant TypeScript SDK

Scan files for malware from Node.js and TypeScript.

## Install

```bash
npm install @detectant-api/sdk
```

Set your API key in the environment:

```bash
export DETECTANT_API_KEY="your-api-key"
```

## Create a client

```ts
import { Detectant } from "@detectant-api/sdk";

const detectant = new Detectant({
  apiKey: process.env.DETECTANT_API_KEY,
});
```

## Scan one file

The simplest Node.js option is a file path:

```ts
const result = await detectant.scan({ path: "./invoice.pdf" });

console.log(result.verdict, result.detections);
```

The call completes after the file has been analyzed and returns its scan result.

### Supported file inputs

Choose the input that already fits your application:

```ts
import { createReadStream, readFileSync } from "node:fs";

// A path — recommended when the file is on disk
await detectant.scan({ path: "./invoice.pdf" });

// A Node.js readable stream
await detectant.scan(createReadStream("./invoice.pdf"));

// A Buffer or Uint8Array already in memory
await detectant.scan(readFileSync("./invoice.pdf"));
await detectant.scan(new Uint8Array([/* file bytes */]));

// A browser File, such as one selected with <input type="file">
await detectant.scan(fileInput.files![0]);

// A Blob
await detectant.scan(new Blob([fileBytes], { type: "application/pdf" }));
```

For in-memory data, add a filename and content type when they are known:

```ts
await detectant.scan({
  data: fileBuffer,
  filename: "invoice.pdf",
  contentType: "application/pdf",
});
```

The SDK accepts file paths, Node.js streams, web `ReadableStream`s, `Buffer`s,
`Uint8Array`s, `ArrayBuffer`s, `Blob`s, and `File`s.

## Scan a batch

Upload between 1 and 20 files. Results are returned in the same order as the inputs.

```ts
const batch = await detectant.scanBatch([
  { path: "./invoice.pdf" },
  { path: "./archive.zip" },
]);

for (const item of batch.results) {
  if (item.scan) {
    console.log(item.filename, item.scan.verdict);
  } else {
    console.error(item.filename, item.error);
  }
}
```

One file can fail without preventing the other files in the batch from being scanned. Check each item's `scan` and `error` values.

## Configuration

Increase the timeout for large files when needed:

```ts
const detectant = new Detectant({
  apiKey: process.env.DETECTANT_API_KEY,
  timeoutInSeconds: 120,
});
```
