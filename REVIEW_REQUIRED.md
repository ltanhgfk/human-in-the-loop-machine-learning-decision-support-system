# Review Required

This file records items that should remain explicit during public-repository review.

## Third-party dependencies

Before redistributing the repository as a public software artifact, verify the applicable
license and provenance information for third-party components documented in
`docs/DEPENDENCIES.md`.

Particular attention should be given to legacy SMS/MMS libraries and Vietnamese NLP
resources whose exact historical versions or licenses may require upstream verification.

## Historical reconstruction

`SimilarityUtil.java` is a 2026 reconstruction of the reported historical cosine-similarity
retrieval design. The original implementation source is no longer available.

The reconstruction is intentionally documented as such and should not be presented as
the original historical source.

## Public-release scope

The public repository excludes private historical data, trained models, runtime credentials,
private communication payloads, database backups, and third-party model resources that are
not necessary for source inspection.

This file is a transparency checklist, not a claim that every historical dependency can be
reproduced from the public repository.
