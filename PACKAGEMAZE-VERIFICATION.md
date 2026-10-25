# PackageMaze production verification

This independent fork verifies Python installation and publication through the
`pm-onboarding-test-20261024/pypi` Feed.

The manual workflow is `.github/workflows/release.yml` on `main`. Its install
and publish permissions are separate. Publication is limited to
`pm-onboarding-test-sampleproject`.

[Run 40135070634](https://github.com/pm-onboarding-test-20261024/sampleproject/actions/runs/40135070634)
passed on 24 October 2026 at commit `4946ac45377d6824752d689d973977731453e734`.
It installed dependencies, ran the upstream tests and built distributions in a
separate job without package credentials, published both distributions, and
installed the exact published version. The downloaded wheel matched the
original bytes.

| Result | Value |
| --- | --- |
| Published version | `4.0.40135070634.dev1` |
| Wheel size | 5,162 bytes |
| Wheel SHA-256 | `165633fa88a8376f67140882bc146473dba371e82e1f91d6f38c218d15fe052a` |
| Source distribution size | 6,074 bytes |
| Source distribution SHA-256 | `cde730d481364f41e270776516b0b93af18cc216c0a5456ecc0f8d744c6f7dd1` |

This test used `uv publish --no-attestations`; it does not claim package
provenance or a PackageMaze Trust evaluation.

The workflow runs only when manually dispatched. Updating this record does
not publish another package version.

## Automatic Project reading

The source expectations in `pyproject.toml` are runtime dependency `peppercorn`,
extra `dev` containing `check-manifest`, extra `test` containing `coverage`, and
a separate Build group containing `setuptools` from `[build-system].requires`.
None of these declarations constrains a version in this fork.

Automatic discovery is verified by a normal GitHub event after a protected
PackageMaze release. Compare every dependency group with this manifest, keep
the existing Project identity, and record waiting time separately from
processing and UI refresh. The first discovery-version refresh is a different
sample from a later source-only update that can reuse its reading. No manual
Rescan or publication workflow is needed for this check.

## First automatic check result

On 25 October 2026, the normal main push at `11b8987884a5734fcadda66419f0781ef906e7a7`
completed automatic discovery after the protected PackageMaze release.
Project 1 retained its identity and showed all four declarations above. The
Build group now contains `setuptools`; the runtime and both extras remained
unchanged.

This was the first refresh after a scanner interpretation change. A subsequent
source-only update should preserve those results while allowing reuse of the
completed reading. No manual Rescan was used.
