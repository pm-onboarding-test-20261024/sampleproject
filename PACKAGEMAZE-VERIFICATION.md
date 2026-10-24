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
