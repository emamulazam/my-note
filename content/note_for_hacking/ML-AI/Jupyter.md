
First you need to make virtual environment

# Virtual Environment

To install environment

```
sudo apt update
sudo apt install python3-venv -y
```

To create environment name `env`

```
python3 -m venv env
```

To activate the environment

```
source env/bin/activate
```

To deactivate

```
deactivate
```

# Install and run

First activate the lab and then

## lab

To install lab

```
pip install jupyterlab
```

To run

```
jupyter lab
```

## notebook

To install lab

```
pip install notebook
```

To run

```
jupyter notebook
```


# Short cut
By ChatGPT

### 🔁 **Two Modes in JupyterLab**

- **Edit Mode** (Green border): When you're typing inside a cell.
    
- **Command Mode** (Blue border): When you're managing cells (Add/Delete/Run).
    

---

### ⌨️ **Shortcuts in Command Mode (Press `Esc` to enter)**

|Shortcut|Action|
|---|---|
|`A`|Insert cell **Above**|
|`B`|Insert cell **Below**|
|`D` `D`|**Delete** selected cell|
|`Z`|**Undo** cell deletion|
|`Y`|Change cell to **Code**|
|`M`|Change cell to **Markdown**|
|`Shift` + `Enter`|**Run** cell & go to next|
|`Ctrl` + `Enter`|Run cell, stay in place|
|`Shift` + `M`|**Merge** selected cells|
|`Up` / `Down`|Move to another cell|
|`X`|**Cut** cell|
|`C`|**Copy** cell|
|`V`|**Paste** below|
|`Shift` + `V`|Paste **above**|
|`L`|Toggle **line numbers**|
|`0` `0`|**Restart** the kernel|

---

### ✏️ **Shortcuts in Edit Mode (Press `Enter` to enter)**

|Shortcut|Action|
|---|---|
|`Ctrl` + `Enter`|Run the cell|
|`Tab`|**Autocomplete** code|
|`Shift` + `Tab`|Show **Docstring/help**|
|`Ctrl` + `/`|**Toggle comment** on selected lines|
|`Ctrl` + `Z`|**Undo**|
|`Ctrl` + `Shift` + `Z`|**Redo**|
|`Esc`|Switch to Command mode|
