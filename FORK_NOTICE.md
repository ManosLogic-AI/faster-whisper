# About this fork

This is an unofficial fork of
[SYSTRAN/faster-whisper](https://github.com/SYSTRAN/faster-whisper). It is not
affiliated with or endorsed by SYSTRAN. Please report issues with
faster-whisper itself upstream.

## What is different

Base: upstream release 1.2.1, commit
`65882eee9f5cdbeeb2d877f1131d48cf241b327d` (tag `v1.2.1`).

The only code change is in `faster_whisper/audio.py`: `import av` is moved
from module level into the three functions that use it (`decode_audio`,
`_ignore_invalid_frames` and `_group_frames`). As a result, importing
`faster_whisper` no longer requires PyAV to be loadable. Decoding audio files
still uses PyAV, and raises the usual error if it is not installed.

Unchanged:

- the public API and transcription behaviour;
- the declared dependencies, including `av`;
- the bundled assets.

The version is set to `1.2.1.post1`, and every release on this fork is
labelled as a build of this fork rather than an upstream release. (A `+label`
local version is not used because GitHub release asset names cannot contain
`+`, and pip reads the version from the wheel file name.)

## License

MIT, as upstream. The original copyright notice and license text are kept in
full in [`LICENSE`](LICENSE).

## Releases

Each release is built from a tag on this fork. Its notes list the upstream
commit, the patched commit, the build tool versions and the SHA-256 of the
wheel. Published release assets are never replaced; any change gets a new
version.

## Updating from upstream

1. Start from the new upstream release tag.
2. Re-apply the lazy-import change to `faster_whisper/audio.py`, and set the
   version to `<upstream version>.post1` (or the next unused `.postN` if the
   same upstream version is patched again).
3. Build the wheel in a clean environment and inspect its contents.
4. Publish it as a new release with its SHA-256. Never overwrite an existing
   release.
