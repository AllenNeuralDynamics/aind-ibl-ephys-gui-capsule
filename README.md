This is the [capsule](https://codeocean.allenneuraldynamics.org/capsule/6044160/tree) that launches the IBL Gui in the image space. The repo that this capsule uses is found here: [aind-ibl-gui](https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui). Duplicate this capsule to start.

### Attaching Data
Before launching the gui, make sure these 2 assets are attached. The output from this capsule: https://codeocean.allenneuraldynamics.org/capsule/0325751/tree, and the stitched SmartSPIM asset for the subject.

### Setting docdb credentials
If you want to save to the metadata database, before launching the workstation follow the steps below:
* Click on the environment tab in the left
* Scroll down to the Secrets section
* Under the drop down choose the one in the screenshot below:
  
  ![image](https://github.com/user-attachments/assets/12222621-ea42-425c-8497-903d8b652f72)

* If you do not see this role in the drop down, reach out to David Feng or Dan Birman to be added

### Environment variables
* Launch the Ubuntu workstation and open the terminal
* Before launching the gui follow run the commands below:
* 
  `export username="YOUR NAME"`. Then press enter<br>

* Then launch the gui and proceed as usual.

### Using the gui
Open up a terminal by hitting the square shaped button in the lower left. CLick on terminal and then type in `launch`. Navigate to the probe you want to load and click on that folder. Once loaded, something like below should show:

![image](https://github.com/user-attachments/assets/fa014933-94fd-4bdf-874f-590a0db362ea)

Usage instructions can be found on the [`iblapps` wiki](https://github.com/int-brain-lab/iblapps/wiki). For debugging, check the terminal for console outputs (where the gui was launched) and reach out to Josh or Arjun if needed. IMPORTANT: If you do not have docdb credentials, the output will still be saved to `/results`. **Make sure to click save before proceeding to next session/probe**.

  
