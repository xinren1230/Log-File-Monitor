# Log-File-Monitor
Monitor the vacuum of IC Titan



Overview
The Log File Monitor is a Windows-based C++ application designed to monitor a specified log file in real time. It reads the latest value from a user-selected parameter (e.g., IGPa, IGPcl, etc.) every second, compares it against a user-defined threshold, and displays the current value in a small, draggable window located at the top-right corner of the screen. If the parameter value exceeds the threshold (or if an error occurs when reading the value), the application will emit a beep sound as an alert.

Features
File Selection:
A file dialog allows you to choose the log file to monitor.

Channel Selection:
The application lists available channels (parameters) such as:
CCGp, IGPa, IGPcl, IGPco, IGPf, PIRbf, PIRll, PIRm, PIRpv, PPcl
The default parameter is IGPcl if no selection is made.

Threshold Setting:
After selecting a channel, you are prompted to enter a threshold value for that channel. A default threshold (1e-6) is provided if no value is entered.

Real-Time Monitoring:
The application reads the log file every second, extracting the value from the selected channel (assumed to be on a specific column based on a fixed header format).

Visual Display:
A small, always-on-top window shows the current parameter value. The value is displayed in:

Green if the value is less than or equal to the threshold.
Red if the value is less than 0 (indicating a read error) or if it exceeds the threshold. The window is draggable by clicking anywhere on it.
Audible Alerts:
When a read error occurs (value < 0) or the value exceeds the threshold, the application emits a beep sound (with different frequencies for error and alert).

System Requirements
Operating System: Windows (the application uses Windows API functions).
Compiler: A C++11 (or later) compliant compiler. For example, Microsoft Visual Studio or MinGW.
Libraries:
<windows.h> and <commdlg.h> for the file dialog and window management.
Standard C++ libraries for file I/O, threading, and string handling.
Building the Application
Ensure C++11 Support:
Make sure your compiler supports C++11 or later. For example, with g++, you can use:

r
Copy
g++ -std=c++11 -o LogMonitor LogMonitor.cpp -mwindows
If you use Visual Studio, set the C++ language standard in the project settings.

Source Code:
Include the source code (e.g., LogMonitor.cpp) along with any additional files.

Compile:
Use your chosen IDE or command-line tools to build the application.

Usage Instructions
Launch the Application:
Run the compiled executable. The application will display a file dialog for you to select the log file.

Select Log File:
Use the file dialog to navigate to and select the log file you want to monitor. Click "Open" to confirm.

Channel Selection:
The console will display a list of available channels:

nginx
Copy
CCGp IGPa IGPcl IGPco IGPf PIRbf PIRll PIRm PIRpv PPcl
When prompted, type the name of the channel you wish to monitor. Press Enter to use the default (IGPcl) if no input is provided.

Threshold Setting:
Next, you will be prompted to enter a threshold value for the selected channel. A default value of 1e-6 is shown. Press Enter to accept the default or type your own threshold value and press Enter.

Monitoring Window:
An always-on-top, draggable window appears in the top-right corner of the screen displaying the current value of the selected channel.

If the current value is within acceptable limits (i.e., ≤ threshold), it is displayed in green.
If the value is negative (indicating an error) or exceeds the threshold, it is displayed in red. The text is updated every second.
Audible Alerts:
If a read error occurs or if the parameter value exceeds the threshold, the application emits a beep sound:

An error beep (500Hz, 300ms) for read errors.
An alert beep (750Hz, 300ms) if the value exceeds the threshold.
Draggable Display:
You can click and drag anywhere on the display window to reposition it on your screen.

Termination:
To exit the application, close the display window (which will also stop the monitoring loop).

Customization
Font and Colors:
You can change the font size, style, and colors by modifying the CreateFontA parameters and the color values in the WM_PAINT handler.

Window Size and Position:
The display window's size and initial position can be adjusted by modifying the parameters in the CreateWindowExA function in the DisplayThread function.

Beep Settings:
The frequency and duration of the beep alerts can be modified by changing the parameters of the Beep function calls.

Log File Format Assumptions:
The application assumes a specific header format where the first three tokens are non-channel information (Event type, Date, Time), and channel data begins from the 4th token onward. If your log file format differs, adjust the column index calculations accordingly.

Troubleshooting
"Failed to read value!" Error:
This message appears if the application cannot extract a valid number from the expected column. Verify that your log file is formatted correctly and that the channel data is in the expected column.

Display Overlap:
If you notice overlapping text, ensure that the background is being cleared properly in the WM_PAINT handler (using FillRect).

Compilation Warnings/Errors:
Ensure that you have set the correct compiler flags (e.g., /D_CRT_SECURE_NO_WARNINGS in Visual Studio or using sprintf_s as shown in the source code).

Contact and Support
For further assistance or to report bugs, please contact the development team or refer to the project's issue tracker (if available).