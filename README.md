# freela-ontap-models

On-device models that the FreelaOnTap iOS apps download after install. The files are published as
GitHub Releases. A published release is never edited: a new model gets a new tag, and the apps pin
the tag, the byte count, and the SHA-256 of the file they install.

## mpnet-fp16-v1

A sentence-embedding model for recommendations on iOS 27, run with Apple's Core AI framework. No
text leaves the device: the app downloads this file once, then embeds profile and job texts locally.

| | |
|---|---|
| Source model | [sentence-transformers/paraphrase-multilingual-mpnet-base-v2](https://huggingface.co/sentence-transformers/paraphrase-multilingual-mpnet-base-v2), revision `4328cf26390c98c5e3c738b4460a05b95f4911f5` |
| Authors | N. Reimers, I. Gurevych (sentence-transformers) |
| License | Apache-2.0, see [LICENSE](LICENSE) |
| Changes | Converted to a Core AI `.aimodel` in float16 with `coreai-torch` 0.4.3. The output is `last_hidden_state` only; the pooler is dropped, and mean pooling runs in the app |
| Output | 768 dimensions, input capped at 128 tokens |
| File | `mpnet-fp16-v1.aar` (Apple Archive, LZFSE) |
| Size | 511,204,319 bytes |
| SHA-256 | `27e2b82ab0a6c1a5c018e78e925117ecc9a0e07e562b8b5d95731f9233a650ce` |

The archive holds one folder:

```
mpnet-fp16-v1/
  model.aimodel/        Core AI program and weights (float16)
  tokenizer/            the source model's stock tokenizer.json and tokenizer_config.json
```

Extract it with `aa extract -i mpnet-fp16-v1.aar -d <dir>` on macOS, or with the `AppleArchive`
framework on iOS. Verify the hash first:

```bash
shasum -a 256 mpnet-fp16-v1.aar
```
