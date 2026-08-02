# Middle Earth — pack files

Download host for [pack-sync](https://github.com/dogtreat268/lotr-pack): the
`manifest.json` every player's launcher reads, and the one jar that has to be
hosted rather than fetched from Modrinth.

Everything else in the pack — Iris, JEI, Sodium — resolves to Modrinth's CDN, so
it is not duplicated here. Only The Lord of the Rings mod lives in `mods/`,
because Modrinth has never heard of it.

Nothing here is edited by hand. Both files are published from the mod's build
repo with `tools/publish.sh --push`, which builds the jar, installs it into the
source Prism instance, and regenerates the manifest from that instance.

## Using it

Point pack-sync's client at the manifest as a Prism **pre-launch command**
(Instance → Settings → Custom commands):

```bash
"$INST_JAVA" -jar /absolute/path/to/sync-client-1.0.0.jar \
  --manifest https://raw.githubusercontent.com/dogtreat268/lotr-pack/main/manifest.json \
  --target "$INST_MC_DIR"
```

The client downloads anything missing or out of date, deletes any `mods/*.jar`
the manifest does not list, and fails the launch rather than starting a client
whose mods do not match the server.

GitHub's raw CDN caches for about five minutes, so a fresh publish takes that
long to reach everyone.
