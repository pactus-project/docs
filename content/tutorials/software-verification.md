---
title: Verify Pactus Software Is Safe
weight: 11
---

## Preface

When downloading Pactus software, it's important to verify that the binaries are authentic and
haven't been tampered with.
By verifying the signatures of the files, you ensure that the software you're installing is secure.
This guide will walk you through the steps to verify Pactus software.

## Understanding the Verification Process

When the Pactus binaries are created, a `SHA256SUMS` file is generated,
containing the checksums (unique digital fingerprints) for the binaries.
This file is then digitally signed and stored in `SHA256SUMS.sig`.
Users can later verify the integrity of the downloaded binaries by
checking the checksums and confirming the validity of the signature.

## Verify the Checksum

Once you've downloaded the binaries and the `SHA256SUMS` file,
run the following command to ensure the binaries match the checksums:

```bash
sha256sum -c SHA256SUMS --ignore-missing
```

This command will compare the checksums in the `SHA256SUMS` file with the ones generated from your downloaded binaries.
If they match, you’ll see an “OK” message, confirming that the files are intact and unaltered.

## Verify the SHA256SUMS Signature

To ensure that the `SHA256SUMS` file itself hasn’t been tampered with,
Pactus signs the file with a digital signature.
You can verify this signature using [Cosign](https://docs.sigstore.dev/cosign/).

```bash
cosign verify-blob SHA256SUMS --signature=SHA256SUMS.sig --key https://pactus.org/cosign.pub
```

This command uses the Pactus public key, hosted at [https://pactus.org/cosign.pub](https://pactus.org/cosign.pub),
to confirm that the Pactus team signed the file.

If the signature is valid, Cosign will confirm that the `SHA256SUMS` file is legitimate and
was signed by the official Pactus team.

## Why This Is Important

By verifying both the checksum and the signature, you ensure:

- The Pactus binaries you downloaded are complete and unmodified.
- The `SHA256SUMS` file has not been tampered with and was signed by the Pactus team.

This process protects your system from potentially compromised software and
ensures you're running the correct, secure version of Pactus.
