
# KiExport

**KiExport** is a Python application for exporting manufacturing files from KiCad PCB design projects. This is a CLI (Command Line Interface) utility. Commands and arguments can be passed to the script while running or from a JSON configuration file named `kiexport.json`. You should be familiar working with CLI tools and how to execute commands from a terminal.

KiExport generates the manufacturing files based on the options available in the `kiexport.json` file, and saves them in an organized way. It renames the files, folders and create ZIP archive files with proper names so that you can send them to a manufacturer or client easily. Since the `kiexport.json` configuration file can be edited for any project, you only have to create the file once. 
The [**Mitayi Pico RP2040**](https://github.com/CIRCUITSTATE/Mitayi-Pico-RP2040) project is added as a sample project to test the script. 

- **Author:** [Vishnu Mohanan](https://github.com/vishnumaiea)
- **Version:** `0.0.22`

This tool was created with the help of [**ChatGPT**](https://chat.openai.com/chat). Thanks to humanity!

## Why?

- Currently, exporting manufacturing files from KiCad's own UI requires setting so many options correctly and moving through different steps for different types of files.
- If you make a mistake in choosing the options correctly, you will end up with a "bad" manufacturing file that will waste your time later.
- KiCad currently has no ability to save the export options as presets and it does not always remember the previously used options.
- Existing plugins available for KiCad only work for specific types of files and specific set of manufacturing options.
- The number and types of files generated from a KiCad project can be quite many. Renaming, organizing and archiving the files manually can be a tedious task. For example, we generate Gerbers, PCB PDF, Schematic PDF, STEP, VRML, CSV BoM, HTML BoM, Position Files, and Preview Images for a typical project. We have to do this every time we make a change to the project to keep consistency across the set of files generated at a time.
- KiCad CLI can do almost all of what the KiCad UI can.
- Instead of typing the arguments manually to a terminal all the time, we can save the options as a JSON file and call the KiCad CLI every time we want to generate the files.

## Requirements

- Python 3.x
- KiCad 8.x
- Git
- Recommended:
  - VS Code
  - Windows Terminal

## Installation

KiExport relies on the [**KiCad-CLI**](https://docs.kicad.org/8.0/en/cli/cli.html) tool to generate the files and therefore supports all the features of KiCad-CLI. You should have a KiCad version installed in your system to use this tool. You can download and install the latest version of KiCad from [here](https://kicad.org/download/). After installation, browse to the installation folder and find the `bin` directory where the `kicad-cli.exe` file is located. Add the `bin` folder to your System Path. If you do not know how to add a new path to the System Path variable, check out any tutorials on the internet.

You can clone/fork the project to obtain a copy of the repository in your system using the following command. Git should be installed and available on the path.

```
git clone https://github.com/vishnumaiea/KiExport.git
```

Additionally, you can download the project as a ZIP file and extract it in your system. After getting the files, you can add the project folder to the System Path. If your system opens Python script files with the Python interpreter by default, you can run any python script directly from the terminal even without using the `.py` extension as shown in the image below.

![Windows Terminal](/resources/2024-10-12_10-05-04-PM-.png)

## Example

Following is a tree view of the files generated by KiExport from the **Mitayi Pico RP2040** project. A top level revision folder will be created to store the files for that specific revision. Under that, a date-specific folder will be created to store files generated in a specific day. Inside that, file-specific folders are created to store the different types of files. ZIP archives are created for some type of files are usually sent as a set of files to the manufacturer, for example Gerbers.

If you generate the files multiple times a day, older files will be overwritten except for any files with a sequence number at the end of the filename. For example, ZIP files have a sequence number at the end of the filename after the date string. A new file with a new sequence number will be created when multiple files are generated.

```
\---R0.6
    \---2024-10-26
        +---3D
        |       Mitayi-Pico-RP2040-R0.6-STEP-26102024-1.step
        |       Mitayi-Pico-RP2040-R0.6-VRML-26102024-1.wrl
        |
        +---Assembly
        |       Mitayi-Pico-RP2040-R0.6-Pos-All.csv
        |       Mitayi-Pico-RP2040-R0.6-Pos-Back.csv
        |       Mitayi-Pico-RP2040-R0.6-Pos-Front.csv
        |       Mitayi-Pico-RP2040-R0.6-Position-Files-26102024-1.zip
        |
        +---BoM
        |       Mitayi-Pico-RP2040-R0.6-BoM-CSV-26102024-1.csv
        |
        +---Gerber
        |       Mitayi-Pico-RP2040-R0.6-B_Courtyard.gbr
        |       Mitayi-Pico-RP2040-R0.6-B_Cu.gbr
        |       Mitayi-Pico-RP2040-R0.6-B_Fab.gbr
        |       Mitayi-Pico-RP2040-R0.6-B_Mask.gbr
        |       Mitayi-Pico-RP2040-R0.6-B_Paste.gbr
        |       Mitayi-Pico-RP2040-R0.6-B_Silkscreen.gbr
        |       Mitayi-Pico-RP2040-R0.6-Edge_Cuts.gbr
        |       Mitayi-Pico-RP2040-R0.6-F_Courtyard.gbr
        |       Mitayi-Pico-RP2040-R0.6-F_Cu.gbr
        |       Mitayi-Pico-RP2040-R0.6-F_Fab.gbr
        |       Mitayi-Pico-RP2040-R0.6-F_Mask.gbr
        |       Mitayi-Pico-RP2040-R0.6-F_Paste.gbr
        |       Mitayi-Pico-RP2040-R0.6-F_Silkscreen.gbr
        |       Mitayi-Pico-RP2040-R0.6-Gerber-26102024-1.zip
        |       Mitayi-Pico-RP2040-R0.6-job.gbrjob
        |       Mitayi-Pico-RP2040-R0.6-NPTH-drl_map.pdf
        |       Mitayi-Pico-RP2040-R0.6-NPTH.drl
        |       Mitayi-Pico-RP2040-R0.6-PTH-drl_map.pdf
        |       Mitayi-Pico-RP2040-R0.6-PTH.drl
        |       Mitayi-Pico-RP2040-R0.6-User_Comments.gbr
        |       Mitayi-Pico-RP2040-R0.6-User_Drawings.gbr
        |
        +---PCB
        |       Mitayi-Pico-RP2040-R0.6-B_Courtyard.pdf
        |       Mitayi-Pico-RP2040-R0.6-B_Cu.pdf
        |       Mitayi-Pico-RP2040-R0.6-B_Fab.pdf
        |       Mitayi-Pico-RP2040-R0.6-B_Mask.pdf
        |       Mitayi-Pico-RP2040-R0.6-B_Paste.pdf
        |       Mitayi-Pico-RP2040-R0.6-B_Silkscreen.pdf
        |       Mitayi-Pico-RP2040-R0.6-Edge_Cuts.pdf
        |       Mitayi-Pico-RP2040-R0.6-F_Courtyard.pdf
        |       Mitayi-Pico-RP2040-R0.6-F_Cu.pdf
        |       Mitayi-Pico-RP2040-R0.6-F_Fab.pdf
        |       Mitayi-Pico-RP2040-R0.6-F_Mask.pdf
        |       Mitayi-Pico-RP2040-R0.6-F_Paste.pdf
        |       Mitayi-Pico-RP2040-R0.6-F_Silkscreen.pdf
        |       Mitayi-Pico-RP2040-R0.6-PCB-PDF-26102024-1.zip
        |       Mitayi-Pico-RP2040-R0.6-User_Comments.pdf
        |       Mitayi-Pico-RP2040-R0.6-User_Drawings.pdf
        |
        \---SCH
                Mitayi-Pico-RP2040-R0.6-SCH-26102024-1.pdf
```

## Usage

You can run the Python script directly from the source folder with the following command. Python should be installed and available on the path.

```
python kiexport.py <command> <arguments>
```

In addition, you can also run the Windows executable `kiexport.exe` with the following command. The `dist` folder should be added to the path in order for this to work.

```
kiexport <command> <arguments>
```

You can automate running multiple commands with a batch script. Refer to the [`export.bat`](/Mitayi-Pico-D1/export.bat) file for an example. Run the script to see KiExport in action.

```bat
@REM @echo off

:: Set variables
set OUTPUT_DIR=Export
set SCH_FILE=Mitayi-Pico-RP2040.kicad_sch
set PCB_FILE=Mitayi-Pico-RP2040.kicad_pcb

:: Execute commands
kiexport sch_pdf -od "%OUTPUT_DIR%" -if "%SCH_FILE%"
kiexport bom -od "%OUTPUT_DIR%" -if "%SCH_FILE%"
kiexport pcb_pdf -od "%OUTPUT_DIR%" -if "%PCB_FILE%"
kiexport gerbers -od "%OUTPUT_DIR%" -if "%PCB_FILE%"
kiexport positions -od "%OUTPUT_DIR%" -if "%PCB_FILE%"

pause
```

## Commands

### `version`

Run the following command to show the version of the tool.

```
kiexport -v
```

```
kiexport --version
```

### `help`

Show the help menu.

```
kiexport -h
```

```
kiexport --help
```

You can include the command to get the help menu of a specific command. For example,

```
kiexport gerbers -h
```

### `gerbers` 

Export Gerbers.

```
kiexport gerbers -if <input_file> -od <output_dir>
```

- `-if`: Path to the input `.kicad_pcb` file. Required.
- `-od`: Path to the output directory. Required.

### `positions`

Export Position or Centroid files for PCB assembly (PCBA).

```
kiexport positions -if <input_file> -od <output_dir>
```

- `-if`: Path to the input `.kicad_pcb` file. Required.
- `-od`: Path to the output directory. Required.

Example:

```
kiexport positions -if "Mitayi-Pico-D1/Mitayi-Pico-RP2040.kicad_pcb" -od "Mitayi-Pico-D1/Export"
```

### `pcb_pdf`

Export the PCB layers as individual PDF.

```
kiexport pcb_pdf -if <input_file> -od <output_dir>
```

- `-if`: Path to the input `.kicad_pcb` file. Required.
- `-od`: Path to the output directory. Required.

Example:

```
kiexport pcb_pdf -if "Mitayi-Pico-D1/Mitayi-Pico-RP2040.kicad_pcb" -od "Mitayi-Pico-D1/Export"
```

### `sch_pdf`

Export the schematic as PDF.

```
kiexport sch_pdf -if <input_file> -od <output_dir>
```

- `-if`: Path to the input `.kicad_sch` file. Required.
- `-od`: Path to the output directory. Required.

Example:

```
kiexport sch_pdf -if "Mitayi-Pico-D1/Mitayi-Pico-RP2040.kicad_sch" -od "Mitayi-Pico-D1/Export"
```

### `ddd`

Export the 3D files.

```
kiexport ddd -if <input_file> -od <output_dir> -t <type>
```

- `-if`: Path to the input `.kicad_pcb` file. Required.
- `-od`: Path to the output directory. Required.
- `-t`: The type of 3D file to export. Possible values are `STEP` and `VRML`. Required.

Example:

```
kiexport ddd -if "Mitayi-Pico-D1/Mitayi-Pico-RP2040.kicad_pcb" -od "Mitayi-Pico-D1/Export" -t STEP
```

### `bom`

Export the bill of materials files.

```
kiexport bom -if <input_file> -od <output_dir> -t <type>
```

- `-if`: Path to the input `.kicad_sch` file. Required.
- `-od`: Path to the output directory. Required.
- `-t`: The type of bill of materials to export. Possible values are `CSV`. Optional.

Example:

```
kiexport bom -if "Mitayi-Pico-D1/Mitayi-Pico-RP2040.kicad_sch" -od "Mitayi-Pico-D1/Export" -t CSV
```

## Configuration File

KiExport supports a JSON configuration file called `kiexport.json`. The name of the file should be exact. The configuration file should be placed in the root folder of your KiCad project where the main `.kicad_sch` and `.kicad_pcb` files are located. Check the `Mitayi-Pico-D1` folder for an example. A copy of the default configuration file is integrated into the script to use as the default one.

To create a configuration file for your own project, add the `project_name`, the required commands under `commands` and the data for those commands under `data`. All keys that starts with `--` are directly passed to the KiCad-CLI and anything that starts with `kie_` is a data for the KiExport application.

## License

This project is licensed under the MIT license.

## References

- [KiCad Command-Line Interface](https://docs.kicad.org/8.0/en/cli/cli.html)
- [Getting Started with KiCad Version 6 : Beginner’s Tutorial to Schematic and PCB Design](https://www.circuitstate.com/tutorials/getting-started-with-kicad-version-6-beginners-tutorial-to-schematic-and-pcb-design/)
- [How to Install KiCad Version 6 and Organize Part Libraries](https://www.circuitstate.com/tutorials/how-to-install-kicad-version-6-and-organize-part-libraries/)
- [How to Get Your KiCad PCB Design Ready for Automated Assembly – KiCad 6 Tutorial](https://www.circuitstate.com/tutorials/how-to-get-your-kicad-pcb-design-ready-for-automated-assembly-kicad-6-tutorial/)
- [How to Get Your KiCad PCB Design Ready for Fabrication – KiCad Version 6 Tutorial](https://www.circuitstate.com/tutorials/how-to-get-your-kicad-pcb-design-ready-for-fabrication-kicad-version-6-tutorial/)

