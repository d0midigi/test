# README

Due April 1st, 5:00pm

You may work with a partner on this assignment.

## Getting Started

{% stepper %}
{% step %}
### Prepare your host repository

On your host machine (not the VM), go to the course assignments directory:

```bash
cd COS461-Public/assignments
```
{% endstep %}

{% step %}
### Pull latest updates

Pull the latest update from Github:

```bash
git pull
```
{% endstep %}

{% step %}
### Reprovision the VM

Reprovision your VM to install necessary packages for this assignment:

```bash
vagrant reload --provision
```
{% endstep %}

{% step %}
### Start Jupyter Notebook on the VM

On the VM, run:

```bash
sudo ~/.local/bin/jupyter-notebook &
```

This will start a new Jupyter notebook server in the background. Even though it is running in the background, it will sometimes print informative messages to the terminal. You can press Enter each time you get a message to get the shell prompt back. To shut down the notebook, run `fg` then press Control-C twice (once to get the confirmation message, another time to skip confirmation).

While the notebook is running, on your host machine, open your browser and go to:

```
http://localhost:8888
```

This should open the Jupyter notebook file selection window. Jupyter notebook is actually running on port 8888 on your Vagrant VM, but you can access it through your host machine browser because the port is being forwarded between the VM and the host machine.

In the file selection window, enter the `assignment4` directory and then open `Assignment4_Notebook.ipynb`. This will open a notebook with the instructions for the rest of the assignment. Work through this notebook from top to bottom and complete the sections marked "TODO."

**Remember to "Save and Checkpoint" (from the "File" menu) before you leave the notebook or close your tab.**
{% endstep %}
{% endstepper %}

{% hint style="info" %}
To stop the notebook gracefully: bring it to the foreground with `fg`, then press Control-C twice.
{% endhint %}

## Jupyter Notebook

Jupyter Notebook (formerly called iPython Notebook) is a browser-based IDE with a cell-based editor.

* Every cell in a notebook can contain either code or text ("Markdown"). Begin editing a cell by double-clicking it.
* Execute the code in a cell (or render the text) by pressing Shift+Enter with the cell selected.
* Global variables and functions are retained across cells.
* Save your work with "Save and Checkpoint" from the "File" menu.
* If your code hangs, interrupt it with "Interrupt" in the "Kernel" menu.
* You can clear all variables and reset the environment with "Restart" in the "Kernel" menu.

The "Help" menu contains additional resources about Jupyter notebooks (including a user interface tour, useful keyboard shortcuts, and links to tutorials).

{% hint style="warning" %}
Be sure to save frequently. Use "Save and Checkpoint" before closing the tab or leaving the notebook.
{% endhint %}

## Submission

Submit your completed `Assignment4_Notebook.ipynb` file on CS Dropbox here:

https://dropbox.cs.princeton.edu/COS461\_S2019/Assignment-4-Passive-Network-Measurement

* Submit only once for both partners.
* Remember to put your names and netids in the marked location at the top of the file.
