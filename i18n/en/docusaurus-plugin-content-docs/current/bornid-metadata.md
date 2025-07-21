---
title: Metadata
sidebar_position: 2
---

# Metadata

BornID Metadata is a core technology that guarantees the provenance and authenticity of digital content. Based on the C2PA standard, this metadata system allows for tracking the entire process from content creation to distribution.

## Overview

The BornID Metadata system securely records the following information:

- **Creation Information**: When, where, and by whom the content was created.
- **Edit History**: All changes made to the content and information about the editing tools.
- **Distribution Path**: The path through which the content was disseminated.
- **Verification Status**: The current integrity status of the content.

## Metadata Structure

### Active Manifest

```json
{
  "active_manifest": "urn:uuid:f6969d4b-5871-468e-b237-e21f8d2cc219",
  "manifests": {
    "urn:uuid:f6969d4b-5871-468e-b237-e21f8d2cc219": {
      "claim_generator": "c2pa-rs/0.46.0",
      "format": "image/jpeg",
      "instance_id": "xmp:iid:626032b0-9050-4084-8af5-81175cdea0cd"
    }
  }
}
```

### Creative Work Information

```json
{
  "assertions": [
    {
      "label": "stds.schema-org.CreativeWork",
      "data": {
        "@context": "https://schema.org",
        "@type": "CreativeWork",
        "author": [
          {
            "name": "Test User",
            "@type": "Person"
          },
          {
            "name": "Test Company",
            "@type": "Company"
          }
        ],
        "when": "2025-06-24T00:02:01Z"
      }
    }
  ]
}
```

### Ingredients Information

```json
{
  "ingredients": [
    {
      "title": "parent",
      "format": "jpg",
      "instance_id": "xmp:iid:7c0c4c00-e968-4a60-aa26-b362793fe6b2",
      "relationship": "parentOf",
      "thumbnail": {
        "format": "image/jpeg",
        "identifier": "self#jumbf=c2pa.assertions/c2pa.thumbnail.ingredient.jpeg"
      }
    }
  ]
}
```

### Content Fingerprint History

```json
"assertions": [
  {
    "label": "c2pa.soft-binding",
    "data": {
      "alg": "com.digicaps.fingerprint.1",
      "blocks": [
          {
            "scope": {},
            "value": "1*{hash_value}"
          }
      ]
    }
  },
]
```

## Digital Signature

### PS256 Signature System

BornID provides strong digital signatures using the RSASSA-PSS with SHA-256 (PS256) algorithm.

**Signature Information:**

```json
{
  "signature_info": {
    "alg": "Ps256",
    "issuer": "DigiCAP Co.,Ltd.",
    "cert_serial_number": "5539112271043283054276207401787004462"
  }
}
```

### Verification Process

:::info Verification Steps

1. **Claim Signature**: Verification of internal validity period and signature validity.
2. **Hash URI Matching**: Check for consistency of hash URIs for all assertions.
3. **Data Hash**: Verification of the integrity of the content data.
4. **Thumbnail Verification**: Validation of thumbnails for the claim and parent content.
   :::

## Verification Results

### Successful Verification Items

```json
{
  "validation_results": {
    "activeManifest": {
      "success": [
        {
          "code": "claimSignature.validated",
          "explanation": "claim signature valid"
        },
        {
          "code": "assertion.dataHash.match",
          "explanation": "data hash valid"
        }
      ],
      "failure": []
    }
  }
}
```

## Security Considerations

### Encryption Strength

- **PS256 Signature**: Provides strong security with RSASSA-PSS with SHA-256.
- **Hash Integrity**: SHA-256 hash verification for all assertions.
- **Certificate Chain**: Ensures reliability through certificates issued by DigiCAP Co.,Ltd.

### Content Tracking

- **UUID-based**: Conflict-free tracking with a globally unique identifier.
- **Relationship Mapping**: Tracks edit history through the `parentOf` relationship.
- **Thumbnail Preservation**: Retains thumbnails for visual comparison before and after edits.

## Supported Formats and Tools

| Component | Version | Supported Feature     | Notes                |
| --------- | ------- | --------------------- | -------------------- |
| **JPEG**  | -       | ✅ Metadata Embedding | JUMBF format support |
| **PNG**   | ✅      | ✅                    | XMP metadata         |
| **MP4**   | ✅      | ✅                    | QuickTime metadata   |

## Real-world Use Cases

### Content Provenance Verification

The following information can be verified by analyzing the manifest:

- **Creation Time**: 2025-06-24 00:02:01 UTC
- **Creator**: Test User (Person), Test Company (Company)
- **Edit History**: History of conversion from original JPG to JPEG exists.

### Integrity Verification

The integrity of the content is guaranteed as all verification items have passed successfully:

- **Signature Verification**: ✅ Passed
- **Hash Matching**: ✅ All assertion hash verifications completed
- **Data Integrity**: ✅ No tampering of original data

---

For more detailed technical specifications, refer to the [C2PA Official Documentation](https://c2pa.org/specifications/specifications/1.3/specs/C2PA_Specification.html).
