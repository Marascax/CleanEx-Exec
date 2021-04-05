CleanEx: Excel Deconstruction & Construction

1. Note on Files

Keep all the files in this directory together. The only file users will interact with is the program executable "CleanEx.exe" 
All other files/subdirectories are dependencies for the executable program to work.


2. Running Cleanex

Open Windows Command Prompt and navigate to the build directory containing the all the program files, including the executable "cleanex.exe"
You can then begin running the program as outlined in the following sections.


3. Deconstruct Mode

Deconstruct mode allows for the break down of excel files for later construction.

To run, use command: cleanex --deconstruct [-e|-d] <path>

--deconstruct: flag signaling program to run deconstruction
-e: run on single excel, path is to .xlsx/.xls file
-d: run on entire directory, path is to directory
<path>: absolute path corresponding to -e/-d argument. If -e is set, it's an absolute path to an excel file. If -d is set, it is an absolute path to a directory 
containing excel file(s).

Ex: cleanex --deconstruct -e "C:\Users\user\path\to\example.xlsx"
Ex: cleanex --deconstruct -d "C:\Users\user\dir\path\with\excels"


3a. Deconstruct Running and Results

While running, the program will output the names of excel file(s) found and attempting to deconstruct. 
After a successful run, the path passed to the program will have a new subdirectory called "cleanex-deconstruct." If the user is running on a single excel, then the
new directory will be in the same directory of the excel file passed.

Within the new directory are subdirectories for all the files deconstructed. Each file directory will contain files needed for construction including a PDF of the
excel file and CSV files of all workbook sheets at the time of deconstructing.

Users can then move "cleanex-deconstruct" however they so choose.


4. Construct Mode

Construct excel files using the broken down excel files created from a previous deconstruct mode execution. This mode is expecting the user to have the directory
created by a CleanEx deconstruction.

To run, use command: cleanex --construct -d <path>

--construct: flag signaling program to run construction
-d: path is to directory
<path>: absolute path leading to a directory containing a "cleanex-deconstruct" subdirectory. This path MUST have the deconstruct directory within it to run (not archived/compressed).


4a. Construct Running and Results

While running, the program will output the names of excel files the program is attempting to construct.
After a successful run, the directory path passed to the program will have a new subdirectory called "cleanex-construct."

Within the new directory are subdirectories for all the files constructed. Each file directory will contain the new excel file a JSON file of metadata information.


5. XLS Files

Due to limited support and binary file complexities, .xls files are (re)constructed as .xlsx as of the current CleanEx version. At time of deconstruction, any .xls file
is exported as a temporary .xlsx file and that .xlsx file is deconstructed and deleted from the file system once deconstruction is done. Original MD5 hash metadata is from the
original .xls file. 


6. Metadata

The JSON metadata file at the end of running construction contains any metadata found within the excel file at the time of deconstruction. Included with that are MD5 hashes for
the original excel file and the newly constructed excel file.

7. Excel Media

Media inside excel files are not replaced into newly constructed files due to limitations of what can be found in the OpenXML architecture. Media, like images, are saved in a subdirectory
named "media" (it will be empty if the file had none). Users can use the PDF for reference of where each media piece was in the original document.