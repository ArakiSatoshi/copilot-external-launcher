# Copilot External Launcher
A Python wrapper to pin Copilot (Bing Chat) to your Taskbar.

https://github.com/ArakiSatoshi/copilot-external-launcher/assets/45124115/700e7585-865e-4fcf-a201-fc0806c10325

---

This launcher acts as a simple link opener that opens Copilot's side panel on Windows 11:

`microsoft-edge:///?ux=copilot&tcp=1&source=taskbar`

The .exe file can be pinned to the Taskbar and do the same as the official implementation does.

# 1. Windows preparations

Before going through the following steps, check for the latest updates in Settings > Windows Update. You also might want to set the "Get the latest updates as soon as they're available" toggle to "On".

## 1.1. Check if you already have Copilot available

Depending on your Windows version, you might already have the toggleable switch for Copilot in the Taskbar settings.

Open Settings > Personalisation > Taskbar > Copilot (preview) > On.

![Taskbar items](images/taskbar-settings.webp?raw=true "Taskbar items")

If you do, set it to "On". *You can skip the next steps since you already have Copilot on your Windows 11.*

## 1.2 Check if Copilot opens with the link

Simply put the following link into your browser's address bar if it's just a normal `https://` link and open it. It doesn't have to be Microsoft Edge.

`microsoft-edge://?ux=copilot&tcp=1&source=taskbar`

*If it doesn't open Copilot but rather opens Microsoft Edge, follow step 1.3. If it does, skip step 1.3 and proceed to step 2.*

## 1.3 Try [ViVeTool](https://github.com/thebookisclosed/ViVe/releases)

1. Download the tool for your platform

https://github.com/thebookisclosed/ViVe/releases

2. Extract the tool
3. Launch Command Prompt
4. Navigate to the folder where the extracted ViVeTool is, for example:

`cd C:\Users\user\Desktop\ViVeTool`

5. Execute the following command that enables Moment 3-specific features:

`vivetool /enable /id:44774629,44776738,44850061,42105254,41655236`

6. Reboot your PC

Check if it made Copilot available on your PC natively:

Open Settings > Personalisation > Taskbar > Copilot (preview)

*If it's there, you can skip the next steps since you already have Copilot on your Windows 11. If it's not, check if the link from step 1.2 opens it.*

`microsoft-edge://?ux=copilot&tcp=1&source=taskbar`

*If it does open Copilot, proceed to step 2. If it doesn't, proceed to step 1.4.*

## 1.4 Switching to the Release Preview channel

In my case, Copilot isn't available on Windows Build 22621.2428 but is available on Windows Build 22631.2428. If the previous steps didn't help and you still can't launch Copilot, switching to the Release Preview channel might let you do it.

<p align="center"><b>Disclaimer.</b></p><p align="center">Keep in mind that you have to enable sending optional diagnostic data to Microsoft to be able to switch to any of the Windows Insider channels. You'll only be able to switch back to the Stable Windows build with the next major version of Windows or by completely reinstalling the system.</p>

1. Open Settings > Windows Update > Windows Insider Programme > Get Started.

2. Follow the instructions and set the channel to *Release Preview*. If the Settings freeze on one of the "Continue" steps, close the Settings app and open it again.

![Release Preview](images/release-preview.webp?raw=true "Release Preview")

3. Reboot your PC and check for any missing updates in Settings > Windows Update (you might have to click "Check for updates").

4. Check if it made Copilot available on your PC natively:

Open Settings > Personalisation > Taskbar > Copilot (preview)

5. *If it's not available in the Taskbar settings, check if the link from step 1.2 opens it.*

`microsoft-edge://?ux=copilot&tcp=1&source=taskbar`

*Now you either have Copilot available natively in your system and don't have to do anything else, or have the Copilot sidebar opening when you follow the link and can proceed to Step 2.*

# 2. Creating a convenient .exe file

Download the copilot.exe file from the repository or build it yourself.

## 2.1. Grabbing the .exe from the repository

Download the copilot.exe from this repository and launch it to ensure it opens Copilot. Pin it to the Taskbar, and now you can access Copilot conveniently.

## 2.2. Build the copilot.exe yourself (optional)

Executing someone else's .exe file might not be desirable, but you can build it yourself. In this example, we'll be using [Miniconda](https://docs.conda.io/projects/miniconda/en/latest/index.html).

1. Download and install [Miniconda](https://docs.conda.io/projects/miniconda/en/latest/index.html):

https://docs.conda.io/projects/miniconda/en/latest/index.html

2. Download the file `copilot.py` from this repository and place it into the `copilot` folder on the Desktop.
3. Find a transparent logo for Copilot, place it in the same `copilot` folder, and rename it to `logo.png`. I can't add the logo to this repository, but a quick Google search with the query "copilot logo png" should help.
4. Launch Miniconda by opening the `Anaconda Prompt (miniconda3)` app in the Start menu.
5. Navigate to the `copilot` folder:

`cd Desktop\copilot`

6. Check if `copilot.py` is working as intended:

`python copilot.py`

7. Create a new conda environment:

`conda create --name pyinstaller python=3.10`

8. Activate the new environment:

`conda activate pyinstaller`

9. Install the necessary packages:

`conda install pyinstaller pillow`

10. Convert the script into a .exe file

`pyinstaller --onefile --noconsole --icon=link.png copilot.py`

11. The resulting copilot.exe file should be in the `copilot\dist` folder. Copy it to a desired location and pin it to the Taskbar.
12. (Optional) Deactivate the environment and delete it:

`conda deactivate && conda remove --name pyinstaller --all -y`
