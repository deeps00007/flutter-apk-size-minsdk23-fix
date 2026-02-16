# Detailed Technical Explanation

## Why Android Changed This Behavior

From API 23 onwards:

- Native libraries are extracted directly from APK without compression.
- This avoids runtime decompression.
- Improves startup performance.

## Tradeoff

| Factor | Compressed | Uncompressed |
|--------|------------|-------------|
| APK Size | Smaller | Larger |
| Startup Time | Slight delay | Faster |

## Why Flutter Apps Grow More

Flutter apps include:
- Flutter engine native binaries
- Multiple architecture builds
- Plugin native libraries

When uncompressed, all architectures increase APK size significantly.

---

## Best Production Strategy

1. Use App Bundles for Play Store.
2. Use ABI splits.
3. Avoid legacy packaging unless distributing direct APK.
