to run a git command on all folders in a directory in windows
```bat
@echo off
set /p git_command="Enter git command: "
for /d %%i in (.\*) do (	
	echo +++++++++++++++++++++++++++++++++++++++++++++++++++++++++
	echo "%%i"
	cd "%%i"
	echo -----------------------------------------------
	echo %git_command%
	%git_command%
	echo -----------------------------------------------
	echo +++++++++++++++++++++++++++++++++++++++++++++++++++++++++
	cd..
)
```
