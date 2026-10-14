# README

Due April 10th, 5:00pm

You may work with a partner on this assignment.

## Getting Started

{% stepper %}
{% step %}
### On the host machine

Go to the course assignments directory:

```bash
$ cd COS461-Public/assignments
```

Pull the latest update from Github:

```bash
$ git pull
```
{% endstep %}

{% step %}
### Reprovision the VM

Reprovision your VM to install necessary packages for this assignment:

```bash
$ vagrant reload --provision
```
{% endstep %}

{% step %}
### Start Jupyter Notebook on the VM

On the VM, run:

```bash
$ sudo ~/.local/bin/jupyter-notebook &
```

This starts a Jupyter notebook server in the background. It may print messages to the terminal; press Enter to get the shell prompt back when that happens. To shut down the notebook, run `fg` then press Control-C twice (once to get the confirmation message, another time to skip confirmation).
{% endstep %}

{% step %}
### Open the notebook from your host machine

While the notebook is running, on your host machine open your browser and go to:

```
http://localhost:8888
```

This opens the Jupyter notebook file selection window. Enter the `assignment5` directory and open `Assignment5_Notebook.ipynb`. Work through the notebook from top to bottom and complete the sections marked "TODO."
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Remember to "Save and Checkpoint" (from the "File" menu) before you leave the notebook or close your tab.
{% endhint %}

## Jupyter Notebook — brief notes

* Jupyter Notebook is a browser-based IDE with cell-based editing.
* Cells can contain either code or text (Markdown). Double-click a cell to edit.
* Execute a cell (or typeset text) with Shift+Enter.
* Global variables and functions persist across cells.
* Save work with "Save and Checkpoint" from the "File" menu.
* If code hangs, use "Interrupt" from the "Kernel" menu.
* To clear all variables and reset the environment, use "Restart" from the "Kernel" menu.
* The "Help" menu contains a user interface tour, useful keyboard shortcuts, and links to tutorials.

## Submission

Submit your completed `Assignment5_Notebook.ipynb` file to the CS Dropbox:

https://dropbox.cs.princeton.edu/COS461\_S2019/Assignment-5-Port-Scan

* Submit only once for both partners.
* Remember to put your names and netids in the marked location at the top of the file.
