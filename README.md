This is the capsule that launches the IBL Gui in the image space. The repo that this capsule uses is found here: [aind-ibl-gui](https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui). Click on the Orange Ububtu icon in cloud workstation to launch the gui. If you want to write your results to the document database, follow the instructions below. Duplicating the capsule is probably the most straightforward workflow for doing the manual alignment. 

### Attaching Data
Before launching the gui, make sure these 2 assets are attached. The output from this capsule: https://codeocean.allenneuraldynamics.org/capsule/0325751/tree, and the stitched SmartSPIM asset for the subject.

### Environment Dependency
Also before launching, check that the gui dependency is on the latest. To do this, click on environment, and make sure it shows as below:
![image](https://github.com/user-attachments/assets/9994e025-c9f4-4a37-86ff-e678b5248ef0)

If it doesn't say latest and shows some commit unique identifier, click on it and remove the identifier, and then click on the checkbox. It should say latest. This will ensure you are on the latest version.

NOTE: If you wish to perfrom alignments in the ccf space, set the dependency to this: `git+https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui.git@ibl-ccf-space-app#egg=ibl-ephys-alignment-gui`. 

### Getting temporary docdb credentials
Currently, any secrets attached to the ubuntu workstation are not available after launching the workstation. This is a temporary workaround. Before launching the workstation follow the steps below
* Click on the environment tab in the left
* Scroll down to the Secrets section
* Click on Add Secret and choose AWS Cloud Credentials
* Under the drop down choose the one in the screenshot below:
  
  ![image](https://github.com/user-attachments/assets/12222621-ea42-425c-8497-903d8b652f72)

* If you do not see this role in the drop down, reach out to David Feng or Dan Birman to be added
* After this has been done, click on the Reproducible Run button. Look at the runs, and there should be a file called env.txt

### Pasting the credentials into Ubuntu
* After that file has been made, click on it
* Take note of these fields: **AccessKeyID**, **SecretAccessKey**, and **Token**
* Then launch the Ubuntu workstation and open the terminal
* Before launching the gui follow run the commands below:

  `export AWS_ACCESS_KEY_ID="PASTE AccessKeyID"`. Then press enter<br>
  `export AWS_SECRET_ACCESS_KEY="PASTE SecretAccessKey"`. Then press enter<br>
  `export AWS_SESSION_TOKEN="PASTE Token"`. Then press enter<br>
  `export AWS_DEFAULT_REGION="us-west-2"`. Then press enter<br>
  `export username="YOUR NAME"`. Then press enter<br>

* Then launch the gui and proceed as usual. IMPORTANT: The temporary credentials are only valid for around **1 hour**. This means that once they expire, you will have to regenerate them with the steps above. This will require you to shut down the Ubuntu workstation. IMPORTANT: You must click save to get your alignments saved to docdb and your credentials have not expired. If they have expired, you will see a forbidden message in the console when you try to save. 

### Using the gui
Open up a terminal by hitting the square shaped button in the lower left. CLick on terminal and then type in `launch`. Navigate to the probe you want to load and click on that folder. Once loaded, something like below should show:

![image](https://github.com/user-attachments/assets/fa014933-94fd-4bdf-874f-590a0db362ea)

Usage instructions can be found on the [`iblapps` wiki](https://github.com/int-brain-lab/iblapps/wiki). For debugging, check the terminal for console outputs (where the gui was launched) and reach out to Josh or Arjun if needed. IMPORTANT: If you do not have docdb credentials, the output will still be saved to `/results` 

  
