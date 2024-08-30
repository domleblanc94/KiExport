


#
### **+05:30 11:10:42 PM 30-08-2024, Friday**

  - Added `generatePcbPdf()` to export the PCB as PDF files. Layers are imported in individual files with the `Edge.Cuts` as the common layer.
  - Added `pcb_pdf` command.
  - New Version `0.0.9`.

#
### **+05:30 10:40:59 PM 30-08-2024, Friday**

  - Added `generatePositions()` to export position/centroid files.
  - Added new command `positions`.
  - New Version `0.0.8`.

#
### **+05:30 09:38:10 PM 30-08-2024, Friday**

  - Added `generateDrills()`.
  - Drill files are now generated with the Gerbers.
  - All files in the Gerber target directory, except ZIP files are now deleted before overwriting. This fixes the rename conflicts.
  - If a ZIP file already exists, the new one will now get a new sequence number. This will keep single set of manufacturing files but multiple ZIP files.
  - New Version `0.0.7`.

#
### **+05:30 02:09:09 AM 30-08-2024, Friday**

  - Generated Gerber files are now renamed with the revision tag after the project name.
  - Gerber files are now compressed into a ZIP file using `zip_all_files()`.
  - New Version `0.0.6`.

#
### **+05:30 12:17:50 AM 30-08-2024, Friday**

  - Added `extract_info_from_pcb()` to extract project information from the KiCad PCB file.
  - Now creates Gerber output directory from project revision, current date and a sequence number.
  - `to_overwrite` in `generateGerbers()` function now controls whether or not to overwrite the existing Gerber files in the target directory.
  - Added `test` command and `test()` function.
  - New Version `0.0.5`.
  
#
### **+05:30 11:39:24 PM 29-08-2024, Thursday**

  - Output directory is now created if it does not exist, in `generateGerbers()` function.
  - KiCad-CLI commands will fail if the output directory does not exist.
  - New Version `0.0.4`.

#
### **+05:30 11:33:55 PM 29-08-2024, Thursday**

  - Added `check_file_exists()` to check is a file exists.
  - Added `extract_project_name()` to extract the project name from the file name. This simply removes the extension.
  - Added `extract_pcb_file_name()` to extract the file name from the path.
  - `generateGerbers()` now prints the KiCad PCB project name.
  - Code running successfully.
  - New Version `0.0.3`.

#
### **+05:30 11:18:09 PM 29-08-2024, Thursday**

  - Added CLI argument parser.
  - Added `parseArguments()`.
  - Added `gerbers` command to export Gerber files.
  - `generateGerbers()` function now accepts the input PCB file name and the output directory path.
  - New Version `0.0.2`.

#
### **+05:30 10:45:47 PM 29-08-2024, Thursday**

  - Gerber files exported successfully.
  - Added `generateGerbers()` function.
  - Added Readme and Changes.
  - Added project info.
  - New Version `0.0.1`.
