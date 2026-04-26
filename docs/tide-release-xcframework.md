# Tide Ghostty XCFramework release process

The `release-xcframework.yml` workflow publishes the two Tide-consumed
artifacts for any pushed tag matching `v*`:

- `GhosttyKit.xcframework.tar.gz`
- `GhosttyKit.xcframework.tar.gz.sha256`

The workflow does not create a GitHub Release object. If a matching
Release does not already exist for the tag, the workflow fails with a
clear error.

## Steps

1. Create the tag locally, for example `git tag v1.2.3`.
2. Create the matching GitHub Release for that same tag in
   `DejaVu-Cyber/tide-ghostty`.
3. Push the tag: `git push origin v1.2.3`.
4. Wait for `.github/workflows/release-xcframework.yml` to finish.
5. Verify the uploaded assets:

```sh
curl -fL <release-asset-url> -o GhosttyKit.xcframework.tar.gz
curl -fL <release-checksum-url> -o GhosttyKit.xcframework.tar.gz.sha256
shasum -a 256 -c GhosttyKit.xcframework.tar.gz.sha256
```

The checksum file is part of the stable contract consumed by Tide.
