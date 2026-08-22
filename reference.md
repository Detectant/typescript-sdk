# Reference
<details><summary><code>client.<a href="/src/Client.ts">scan</a>(file) -> DetectantApi.Scan</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Uploads one file and synchronously runs content-type and malware analysis.
Only the first multipart part named `file` with a filename is
scanned; other parts are ignored. Free accounts accept files up to
50 MiB; Grow and Scale accounts accept files up to 250 MiB.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.scan(createReadStream("path/to/file"));

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**file:** `core.file.Uploadable` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `Detectant.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.<a href="/src/Client.ts">scanBatch</a>(files) -> DetectantApi.ScanBatchResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Uploads between 1 and 20 files in repeated `files` multipart parts. Each
file uses its account plan's 50 MiB or 250 MiB per-file limit, validation, content-type
analysis, malware detection, persistence, usage accounting, and billing path
as `createScan`. The encoded multipart request limit is the plan's
per-file limit × 20 plus 1 MiB for multipart framing.

Results preserve submitted-file order. File-level validation or scanner
failures are returned in the corresponding result and do not prevent
other files from being scanned. The whole request is rejected only for
request-level failures such as invalid multipart data, authentication or
rate-limit failure, more than 20 files, or an oversized total request.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.scanBatch([createReadStream("path/to/file")]);

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**files:** `core.file.Uploadable[]` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `Detectant.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Health
<details><summary><code>client.health.<a href="/src/api/resources/health/client/Client.ts">getLiveness</a>() -> DetectantApi.HealthResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns successfully while the API process can serve requests.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.health.getLiveness();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `HealthClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.health.<a href="/src/api/resources/health/client/Client.ts">getReadiness</a>() -> DetectantApi.HealthResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Checks the database, schema, scanner signatures, and scanning dependencies.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.health.getReadiness();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**requestOptions:** `HealthClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Scans
<details><summary><code>client.scans.<a href="/src/api/resources/scans/client/Client.ts">listScans</a>({ ...params }) -> DetectantApi.ScanList</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns scans owned by the authenticated account in descending creation order.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.scans.listScans();

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `DetectantApi.ListScansRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ScansClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.scans.<a href="/src/api/resources/scans/client/Client.ts">getScan</a>({ ...params }) -> DetectantApi.Scan</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns one scan owned by the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```typescript
await client.scans.getScan({
    scan_id: "scan_0123456789abcdef0123456789abcdef"
});

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `DetectantApi.GetScanRequest` 
    
</dd>
</dl>

<dl>
<dd>

**requestOptions:** `ScansClient.RequestOptions` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

