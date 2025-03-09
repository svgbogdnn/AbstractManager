# AbstractManager

A tool for managing markdown notes created in `Obsidian` and `Visual Studio Code`.

## Overview

This project gathers lecture notes from various directories (as specified), integrates files and images, and then pushes them into designated branches of your Git repository containing your lecture materials.

## How to Create Lecture Notes

Use `Obsidian` or `Visual Studio Code` along with Markdown to efficiently document online lectures.

1. Markdown supports the direct inclusion of `LaTeX` formulas within the text, offering a simpler alternative to traditional LaTeX editors.
2. Both `Obsidian` and `Visual Studio Code` enable rapid image insertion—just press `Ctrl+V` to paste a screenshot into your note (the image file is automatically saved in the same folder).

This utility handles the upload of new notes and the management of image files:

1. The **DEFAULT** option uploads your notes exactly as saved.
2. The **PRETTIER** option organizes all screenshots into an `/images` folder and prevents filename conflicts.

## Configuration

Create a `config.json` file in the root directory of the project, modeled after `config.json.example`.

- The `Repo` field should conclude with `.git`.
- Generate a `Personal access token` via your GitHub settings (ensure it grants access to private repositories and workflows).
- For every branch listed under `Branches`, supply the subject name and the **absolute** path to the folder containing your notes.

**Note:** For Windows, replace any `\\` path separators with `/`.

## Running the Tool

1. Ensure Python is installed on your system.
2. Clone the repository:

    git clone https://github.com/svgbogdnn/AbstractManager

3. Navigate to the project root, set up a virtual environment, and install the dependencies:

    cd ./ConspectManager

    # Create and activate the virtual environment
    python -m venv env
    . ./env/Scripts/activate

    # Install required packages
    pip install -r requirements.txt

4. Verify that `config.json` in the project root is correctly filled out.
5. Run the main script:

    python basic.py

6. Check the `basic.log` file to confirm that the push operations were successful. For each `COURSE_NAME`, you should see log messages like:

    DATE TIME; COURSE_NAME; INFO; DEFAULT: push done
    DATE TIME; COURSE_NAME; INFO; PRETTIER: push done

## Setting Up Windows Task Scheduler

1. Launch `Windows Task Scheduler` and create a new task named `AbstractManager`.
2. Select the option to “Run whether user is logged on or not.”

3. Under `Actions`, click `New` and specify the Python interpreter from your virtual environment as the program/script, with the project's `basic.py` file as an argument.

   _For example, on my system:_

   - Python interpreter path:
     C:\Users\YourUsername\Downloads\AbstractManager\env\Scripts\python.exe
   - Script path:
     C:\Users\YourUsername\Downloads\AbstractManager\basic.py


4. Under `Triggers`, create a new trigger and set the desired schedule for checking and uploading your notes (e.g., daily at `0:00:00`).

5. In `Conditions`, ensure that the task will only run when there is an active network connection.

6. In `Settings`, select “Run task as soon as possible after a scheduled start is missed.”


## Setting Up on Linux

For Linux systems, use `crontab` to schedule the task. (Detailed instructions may be provided in a future update.)
