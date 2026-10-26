# Required game data: Fortune

The tested profile is **CUSA04555 / 01.19**. A matching base game **plus**
that update is required; a base-only dump and another edition's files are not
interchangeable. Optional DLC is not required for the build or normal launch.

## Recorded local package inputs

| Role | Recorded package filename | Version / identity |
|---|---|---|
| Base |Dead.or.Alive.Xtreme.3.Fortune.PS4-CUSA04555-[DLPSGAME.COM].pkg|01.00, CATEGORY gd, HP0106-CUSA04555_00-DOAX300000000000|
| Update |DEAD.OR.ALIVE.Xtreme.3.Fortune.Update.v1.19.PS4-DUPLEX-[DLPSGAME.COM].pkg|01.19, CATEGORY gp, same content identity|

Base package SHA256:c40bc71e32930920baed49b24b54b004723876dacabd17c3c1ace40620fd78a7.
Update package SHA256:d92baa7048a381fb17511021b5d367ff9eedbc5c59ab134aad4508e83ee81b45.
Tested merged eboot.bin SHA256:
9c28b12d38f68f7e759149de5b69dab538b6e3b8f9177dfb4bdb351823132bec.

The validation installation used73 optional matching add-on packs. Their
successful file opens do not establish every DLC costume/scene works.
The merged base+update+DLC tree had11287 files / 41457406640logical bytes.

Filenames are local provenance labels, not a requirement to obtain a particular
third-party repack. No game download links or package payloads are provided.
A lawful equivalent dump must match the required title/version and supported
plaintext executable layout.

## Assemble already extracted files

Extract the base and update separately using your own lawful dump/extraction
workflow. Give the helper the roots that contain eboot.bin and sce_sys/param.sfo
(for extraction tools with a uroot/ directory, pass that uroot directory).

```powershell
python tools/Merge-Game.py --base "./inputs/base/uroot" --update "./inputs/update/uroot" --output "./game/CUSA04555"
```

The output must be a new folder. The helper checks title/category/update
metadata, copies the full base tree and overlays the matching update. Preserve
all numbered chunk directories, archives, executables and sce_sys metadata;
mixing one edition's executable with the other edition's assets caused earlier
boot/rendering failures.

For optional matching add-ons, add --dlc followed by each extracted DLC root.
Each pack is placed under addcont/ plus its16-character CONTENT_ID suffix.
Example final layout:

```text
CUSA04555-merged/
  eboot.bin
  sce_sys/param.sfo           # TITLE_ID=CUSA04555; APP_VER=01.19
  sce_module/libc.prx
  sce_module/libSceFios2.prx
  00/ ...                    # preserve all other original chunk directories
  addcont/                   # optional
    CONTENT_LABEL_16/
      sce_sys/param.sfo
      ...original DLC files...
```

Supply libSceFiber.sprx, ulobjmgr.sprx and libSceUlt.sprx separately under
sys_modules/, or pass --modules-dir. The repository does not extract/decrypt
firmware or packages and does not include these modules.

The launcher's offline full-SKU profile is a runtime metadata setting, not a
license or entitlement grant. Installing DLC files does not necessarily unlock
progression-gated/unowned costumes or restore PSN services.
