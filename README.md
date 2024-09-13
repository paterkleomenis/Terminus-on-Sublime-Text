# Terminus-on-Sublime-Text

## Introduction

This repository provides instructions for setting up and using the Terminus plugin in Sublime Text to run Python and C commands directly from within the editor. Terminus is a versatile terminal emulator that integrates seamlessly with Sublime Text, enhancing your development workflow.

## Requirements

- [Sublime Text](https://www.sublimetext.com/)
- Terminus plugin
- Python interpreter
- GCC compiler (for C)


### Install Terminus Plugin

1. Open Sublime Text.
2. Go to `Preferences` > `Package Control`.
3. Select `Install Package`.
4. Search for `Terminus` and install it.
5. Restart Sublime Text.

### Install Python and C Compilers

1. Ensure Python and GCC are installed on your system.
2. Add them to your system PATH if they are not already configured.

## Configuration

#### C

1. Create a new build system in Sublime Text:
   - Go to `Tools` > `Build System` > `New Build System`.
   - Add the following configuration:

    ```json
    {
    "target": "terminus_exec",
    "cancel": "terminus_cancel_build",
    "shell_cmd": "gcc "${file}" -o "${file_path}/${file_base_name}" && "${file_path}/${file_base_name}"",
    "working_dir": "${file_path}",
    "file_regex": "^(..[^:]):([0-9]+):?([0-9]+)?:? (.)$",
    "selector": "source.c",
    "variants": [
        {
            "name": "Run",
            "target": "terminus_exec",
            "cancel": "terminus_cancel_build",
            "shell_cmd": "gcc "${file}" -o "${file_path}/${file_base_name}" && "${file_path}/${file_base_name}""
        }
      ]
    } 

    ```

   - Save the file as `C_Terminus.sublime-build`.

#### Python

1. Create a new build system in Sublime Text:
   - Go to `Tools` > `Build System` > `New Build System`.
   - Add the following configuration:

    ```json
    {
    "shell_cmd": "python3 \"${file}\"",
    "working_dir": "${file_path}",
    "selector": "source.python",
    "target": "terminus_exec",
    "cancel": "terminus_cancel_build",
    "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
    "variants": [
        {
            "name": "Run",
            "target": "terminus_exec",
            "cancel": "terminus_cancel_build",
            "shell_cmd": "python3 \"${file}\""
        }
      ]
    }
    ```

   - Save the file as `Python_Terminus.sublime-build`.


### Running Code

1. Open a file.
2. Select `Tools` > `Build System` > `Python_Terimus`. (Example)
3. Run the build command (`Ctrl+B` or `Cmd+B`).


