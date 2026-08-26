This is the [capsule](https://codeocean.allenneuraldynamics.org/capsule/6044160/tree) that launches the IBL Gui in the image space. The repo that this capsule uses is found here: [aind-ibl-gui](https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui). Duplicate this capsule to start.

> **Debugger branch.** This branch adds a pre-configured **VS Code debug session** against an editable checkout of the GUI at `/scratch/ibl-ephys-alignment-gui`, for setting breakpoints and stepping through the GUI code on the Code Ocean desktop. Nothing opens at login — start the GUI, the debugger, or a sync from their desktop icons. See [Using the GUI](#using-the-gui) below.

### Attaching Data
Before launching the gui, make sure these 2 assets are attached. The output from this capsule: https://codeocean.allenneuraldynamics.org/capsule/0325751/tree, and the stitched SmartSPIM asset for the subject.

### Setting docdb credentials
If you want to save to the metadata database, before launching the workstation follow the steps below:
* Click on the environment tab in the left
* Scroll down to the Secrets section
* Under the drop down choose the one in the screenshot below:
  
  ![image](https://github.com/user-attachments/assets/12222621-ea42-425c-8497-903d8b652f72)

* If you do not see this role in the drop down, reach out to David Feng or Dan Birman to be added

### Username for docdb
The first time you launch the workstation, a dialog will prompt for a username. This is what gets recorded with alignments saved to docdb. The value is cached on `/scratch` and reused on subsequent runs of the capsule, so you only enter it once. Leave it blank to skip docdb writes (alignments still save to `/results`).

To change it later, delete `/scratch/.ibl-gui-username` and relaunch, or `export username="..."` in a terminal before invoking `launch-ibl-gui`. The username applies whether you run the GUI normally or under the debugger.

### Debugging the GUI
Double-click the **"Debug IBL GUI"** desktop icon to open VS Code on the checkout (`/scratch/ibl-ephys-alignment-gui`) with a debug configuration already set up. Press <kbd>F5</kbd> (or Run → Start Debugging) and pick **"Debug: IBL Ephys Alignment GUI"** to launch `scripts/launch.py` under the debugger — set breakpoints anywhere in the GUI or `iblatlas` (`justMyCode` is off).

VS Code opens inside a terminal window that stays open, so if the editor fails to launch you can read the error there.

Notes on the debug config (`.vscode/launch.json`):
* The GUI is installed **editable** from the checkout, so the source you edit is the code that runs — breakpoints anywhere in the tree bind.
* It runs the system interpreter at `/opt/conda/bin/python`, where the GUI is installed — there is no separate project venv.
* PyQt5 + debugpy needs `PYDEVD_USE_FRAME_EVAL=NO` (set in the config) so breakpoints in Qt slots/threads actually fire on CPython 3.10; leave it in place.

### Syncing upstream changes (no rebuild)
The checkout lives at `/scratch/ibl-ephys-alignment-gui`, which **persists across capsule runs**, and it is installed editable. To pull the latest upstream code and reinstall **without rebuilding the capsule**, double-click the **"Sync IBL GUI"** desktop icon (or run `sync-ibl-gui` in a terminal), then restart the debug session (<kbd>F5</kbd>). Pure-Python changes take effect on the next run; dependency changes are picked up by the reinstall.

* `sync-ibl-gui` does `git pull --ff-only` + editable reinstall. If you have local edits that block a fast-forward, it stops and tells you to resolve them in `/scratch/ibl-ephys-alignment-gui` first — it won't clobber your work.
* Your local edits and the pulled version survive workstation stop/resume (they're on `/scratch`). `/opt/conda` does not, so an autostart re-creates the editable install at each session start; without it `launch` would silently run the image-baked copy instead of your checkout. If that repair fails you get an error dialog, and the details land in `/scratch/.ibl-gui-relink.log`.
* A capsule rebuild is still what refreshes the **baked** baseline (and the heavy dependency cache). Delete `/scratch/ibl-ephys-alignment-gui` to reset the checkout to that baseline.

#### Debugging a different branch
Point the checkout at any branch with `sync-ibl-gui <branch>`, e.g.:

```bash
sync-ibl-gui fix/histology-offsets   # fetch + switch + editable reinstall
```

This creates a local tracking branch from `origin/<branch>` the first time, pulls it, and reinstalls. The selected branch **persists on `/scratch`**, so restart the debug session (<kbd>F5</kbd>) and every subsequent launch (debug or plain) uses it — no rebuild, no config change. Run bare `sync-ibl-gui` afterwards to pull further updates on that branch, or `git -C /scratch/ibl-ephys-alignment-gui checkout <branch>` for full manual control. Switching is refused if you have uncommitted edits (commit/stash them first).

### Using the gui
To run the GUI **without** the debugger, double-click the **"Launch IBL GUI"** desktop icon (or run `launch-ibl-gui` in a terminal). This runs whatever `sync-ibl-gui` last installed, so you can stay on this branch, sync, and launch normally without ever opening VS Code. A terminal window opens and runs the GUI; if it exits or crashes, the terminal stays open so you can read the traceback and rerun `launch-ibl-gui` there.

Navigate to the probe you want to load and click on that folder. Once loaded, something like below should show:

![image](https://github.com/user-attachments/assets/fa014933-94fd-4bdf-874f-590a0db362ea)

Usage instructions can be found on the [`iblapps` wiki](https://github.com/int-brain-lab/iblapps/wiki). For debugging, use the VS Code session above, or check the terminal for console outputs; reach out to Josh or Arjun if needed. IMPORTANT: If you do not have docdb credentials, the output will still be saved to `/results`. **Make sure to click save before proceeding to next session/probe**.

  
