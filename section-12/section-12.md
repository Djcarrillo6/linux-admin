How to solve these challenges:

To be consistent with the filenames and paths run the commands on Ubuntu

Write your solution in a terminal and test it.

If your solution is not correct, then try to understand the error messages, watch the video again, rewrite the solution, and test it again. Repeat this step until you get the correct solution.

Save the solution in a file for future reference or recap.



Challenge #1

List all running processes.

Check if a process named bash is running (use both ps and pgrep).



Challenge #2

Using the ps command list all processes sorted by memory in reverse order.

Redirect the output to a file called processes.txt



Challenge #3

Start top, sort processes by CPU, and highlight the running processes and the sorting column.



Challenge #4

Generate a text file that contains 3 runs (refreshes) of top with a delay of 1second.



Challenge #5

Install htop and start it.



Challenge #6

Using the kill command send the default signal (SIGTERM - 15) to the current terminal.



Challenge #7

Start a graphical application like gedit or firefox.

Find its PID and send the SIGINT (2) signal to the application.



Challenge #8

Start a graphical application like gedit from a terminal in the background.

Kill the application using pkill.



Challenge #9

Run a command that takes some time to complete like ls -lR / in the foreground. After a few seconds stop (pause) the command by pressing Ctrl + Z.

Print its JOBID and PID and resume the command in the foreground.



Challenge #10

Run sleep 100 in the background.

Close the terminal, open it again and check if the process is still running.

If it’s not running, run sleep 100 again making it immune to the closing terminal.