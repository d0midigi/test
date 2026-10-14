# README

Due March 18th, 5:00pm

You should work with a partner on this assignment.

## Getting Started

{% stepper %}
{% step %}
### On your host machine

Open the course assignments directory:

```bash
cd COS461-Public/assignments
```

Pull the latest updates from GitHub:

```bash
git pull
```
{% endstep %}

{% step %}
### Reprovision the VM

Reprovision your VM to install the necessary packages for this assignment:

```bash
vagrant reload --provision
```
{% endstep %}

{% step %}
### Prepare the VM environment

Shell into your VM, then uninstall any existing versions of Jupyter and matplotlib:

```bash
sudo pip uninstall matplotlib
sudo pip uninstall jupyter
```

Re-install Jupyter and matplotlib with the --user flag:

```bash
pip install --user matplotlib
pip install --user jupyter
```
{% endstep %}

{% step %}
### Start Jupyter Notebook on the VM

On the VM, run:

```bash
sudo ~/.local/bin/jupyter-notebook &
```

This starts a Jupyter notebook server in the background. The process may print messages to the terminal; press Enter when you see them to get the shell prompt back. To shut down the notebook, run `fg` then press Control-C twice (once to get the confirmation message, another time to skip confirmation).
{% endstep %}

{% step %}
### Access the notebook from your host machine

While the notebook is running, in your host machine browser go to:

```
http://localhost:8888
```

This opens the Jupyter file selection window. Port 8888 on the VM is forwarded to your host, allowing access from your host browser.
{% endstep %}

{% step %}
### Open the assignment notebook

In the Jupyter file selection window:

* Enter the `assignment3` directory.
* Open `Assignment3_Notebook.ipynb`.
* Work through the notebook from top to bottom and complete the sections marked "TODO."

Remember to use "Save and Checkpoint" (from the "File" menu) before you leave the notebook or close your tab.
{% endstep %}
{% endstepper %}

## Jupyter Notebook usage notes

Jupyter Notebook (formerly called iPython Notebook) is a browser-based IDE with a cell-based editor.

* Every cell in a notebook can contain either code or text ("Markdown").
* Begin editing a cell by double-clicking it.
* Execute the code in a cell (or typeset the text) by pressing Shift-Enter with the cell selected.
* Global variables and functions are retained across cells.
* Save your work with the "Save and Checkpoint" option in the "File" menu.
* If your code hangs, you can interrupt it with the "Interrupt" option in the "Kernel" menu.
* You can also clear all variables and reset the environment with the "Restart" option in the "Kernel" menu.

The "Help" menu contains many additional resources about Jupyter notebooks (including a user interface tour, useful keyboard shortcuts, and links to tutorials).

## Submission

Submit your completed `Assignment3_Notebook.ipynb` file on CS Dropbox here:

https://dropbox.cs.princeton.edu/COS461\_S2019/Assignment-3-TCP-Congestion-Control-and-Bufferbloat

* Submit only once for both partners.
* Put your names and netids in the marked location at the top of the notebook file.
* Also submit a `partners.txt` file that contains only your netIDs, one per line.

Acknowledgement

This assignment is modeled after a similar assignment at Stanford University:

http://web.stanford.edu/class/cs244/pa1.html
