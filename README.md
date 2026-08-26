This is the [capsule](https://codeocean.allenneuraldynamics.org/capsule/6044160/tree) that launches the IBL Gui in the image space. The repo that this capsule uses is found here: [aind-ibl-gui](https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui). Duplicate this capsule to start.

> **Autolaunch branch.** The GUI is installed **editable** from a checkout at `/scratch/ibl-ephys-alignment-gui` that tracks the GUI repo's `main`. At every session start the workstation pulls upstream and launches the GUI in a terminal that stays open, so you see which commit you got and any traceback. No capsule rebuild is needed to pick up upstream changes, and no VS Code is installed — use the debugger branch for that.
>
> `sync-ibl-gui` pulls and reinstalls on demand; `sync-ibl-gui <branch>` switches the checkout to another branch, and that choice persists across runs. Local edits in the checkout survive stop/resume and block the auto-pull rather than being clobbered.

### Attaching Data
Attach the preprocessed mouse output and the external assets named in its
`datapackage.json` registry. These commonly include the subject's stitched
SmartSPIM registration asset and `spim_template_to_ccf`; a separate
registration asset may also be needed. Keep complete ephys collections,
including QC files and `band_corr/`, rather than copying only JSON-listed files.

The workstation sets `IBL_ASSET_ROOTS=/data` so external references resolve
against attached assets by recorded name or ID. Renamed mounts need
`IBL_ASSET_CONFIG` or `IBL_ASSET_OVERRIDES`; configure these in the terminal
session before relaunching if needed. Choosing an input directory does not
configure external asset roots. See the GUI's
[portable input contract](https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui/blob/main/docs/input_datapackage_contract.md)
for resolution rules and desktop examples. The resolver locates existing
files; it does not fetch external assets automatically.

### Setting docdb credentials
If you want to save to the metadata database, before launching the workstation follow the steps below:
* Click on the environment tab in the left
* Scroll down to the Secrets section
* Under the drop down choose the one in the screenshot below:
  
  ![image](https://github.com/user-attachments/assets/12222621-ea42-425c-8497-903d8b652f72)

* If you do not see this role in the drop down, reach out to David Feng or Dan Birman to be added

### Username for docdb
The first time you launch the workstation, a dialog will prompt for a username. This is what gets recorded with alignments saved to docdb. The value is cached on `/scratch` and reused on subsequent runs of the capsule, so you only enter it once. Leave it blank to skip docdb writes (alignments still save to `/results`).

To change it later, delete `/scratch/.ibl-gui-username` and relaunch, or `export username="..."` in a terminal before invoking `launch-ibl-gui`.

### Choosing the GUI version
Each time the GUI launches, it installs the version named in `code/gui_version` (`/code/gui_version` in the workstation). The default, `latest`, follows the newest [release](https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui/releases), so a duplicated capsule picks up new releases without a rebuild. To stay on one version, replace it with a release tag such as `v0.4.0`; a branch name or commit of the GUI repo also works. The terminal prints the version it is running, and saved alignments record it. If the install fails, for example without network access, the GUI starts with the version built into the capsule.

### Using the gui
The GUI starts automatically when the Ubuntu workstation finishes booting — a terminal window opens, pulls the latest GUI, and runs `launch-ibl-gui`. If the GUI exits or crashes, the terminal stays open so you can read the traceback; rerun `launch-ibl-gui` in that same terminal to relaunch without restarting the session.

Open the mouse directory containing `datapackage.json`, then select a recording,
ephys collection, and shank in the GUI. Once loaded, something like below
should show:

![image](https://github.com/user-attachments/assets/fa014933-94fd-4bdf-874f-590a0db362ea)

Usage instructions can be found on the [`iblapps` wiki](https://github.com/int-brain-lab/iblapps/wiki). For debugging, check the terminal for console outputs (where the gui was launched) and reach out to Josh or Arjun if needed. IMPORTANT: If you do not have docdb credentials, the output will still be saved to `/results`. **Make sure to click save before proceeding to next session/probe**.

  

## Development

See [CONTRIBUTING.md](CONTRIBUTING.md) for developer setup, checks, and
repository conventions. Coding agents should also read [AGENTS.md](AGENTS.md).
