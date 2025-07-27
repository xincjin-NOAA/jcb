# How `jcb render temp.yaml dest.yaml` Works

The `jcb render` command processes a template file (`temp.yaml`) using the Jinja2 templating engine to produce a final YAML configuration file (`dest.yaml`). Here's a step-by-step breakdown of the process:

### 1. Command-Line Entry Point

- The command is defined in [setup.cfg](cci:7://file:///Users/xjin/my_home/git/jcb/setup.cfg:0:0-0:0), which points the [jcb](cci:1://file:///Users/xjin/my_home/git/jcb/src/jcb/driver.py:9:0-28:8) console script to the [main](cci:1://file:///Users/xjin/my_home/git/jcb/src/jcb/driver.py:62:0-66:16) function in [src/jcb/driver.py](cci:7://file:///Users/xjin/my_home/git/jcb/src/jcb/driver.py:0:0-0:0).
- This script uses the `click` library to define the command-line interface and its subcommands, including [render](cci:1://file:///Users/xjin/my_home/git/jcb/src/jcb/driver.py:34:0-56:74).

### 2. Argument Parsing and File Loading

- The [render](cci:1://file:///Users/xjin/my_home/git/jcb/src/jcb/driver.py:34:0-56:74) function in [src/jcb/driver.py](cci:7://file:///Users/xjin/my_home/git/jcb/src/jcb/driver.py:0:0-0:0) accepts two arguments: `dictionary_of_templates` (your `temp.yaml`) and `jedi_yaml` (your `dest.yaml`).
- It opens `temp.yaml` and loads its contents into a Python dictionary.

### 3. Core Rendering Logic

- The script then calls the main `jcb.render()` function, which is located in [src/jcb/renderer.py](cci:7://file:///Users/xjin/my_home/git/jcb/src/jcb/renderer.py:0:0-0:0). This is where the core work happens:
    - A [Renderer](cci:2://file:///Users/xjin/my_home/git/jcb/src/jcb/renderer.py:34:0-240:24) class is instantiated. Its constructor uses the dictionary from `temp.yaml` to configure paths where the Jinja2 templating engine will look for template files (files ending in `.j2`).
    - Your `temp.yaml` must specify an `algorithm` key. The renderer uses this key to identify the main template file to start with (e.g., `my_algorithm.yaml.j2`).
    - Jinja2 renders this main template. The template can include other templates and uses all the key-value pairs from your `temp.yaml` to fill in variables and control logic within the templates.
    - The final result of the rendering process is a single, complete YAML configuration returned as a string.

### 4. Writing the Output

- The [driver.py](cci:7://file:///Users/xjin/my_home/git/jcb/src/jcb/driver.py:0:0-0:0) script takes this final YAML string, loads it back into a dictionary, and then writes it to your specified destination file, `dest.yaml`.

In summary, [jcb](cci:1://file:///Users/xjin/my_home/git/jcb/src/jcb/driver.py:9:0-28:8) is a specialized tool that uses a primary YAML file (`temp.yaml`) to control the rendering of a hierarchy of Jinja2 templates, producing a final, complete YAML file (`dest.yaml`) for use with the JEDI system.
:wq
