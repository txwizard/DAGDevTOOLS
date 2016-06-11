                             External Tools ReadMe

================================================================================

The pre and post build tesks and the test scripts found in the /scripts
directory of most of my projects use a number of tools that I have developed
over many years. Since they live in a directory that is on the PATH list on my
development machines, they are "just there" when I need them, and I seldom give
them a second thought. For anybody who wants to run the test scripts or build
the project, they are in DAGDevTOOLS.ZIP, which can be extracted into any
directory that happens to be on your PATH list. None of them requires
installation, none of the DLLs is registered for COM, and none of them or their
DLLs use the Windows Registry.

A few use MSVCR120.dll, which is not included, but you probably have it if you
have a compatible version of Microsoft Visual Studio. The rest use MSVCRT.DLL,
which ships with Microsoft Windows.

This kit is made available under a freeware license, contained in LICENSE.TXT.

The following table lists and briefly describes the programs and scripts that
are included in the archive.

Program or Script Name      Purpose
--------------------------- ----------------------------------------------------
Date2FN.exe                 Format the local time as YYYYMMDD_HHMMSS, and append
                            it to the base name of a file. This is a simple way
                            to guarantee unique names for sets of log files and
                            test reports that are easy to sort by creation date.

wwBldNbrMgr.exe             Increment the build number in the AssemblyInfo.cs OF
                            a project. Only C# projects are supported.

WWLogger.exe                Create or append to a text long, each entry having a
                            time stamp.

                            The default format is YYYY/MM/DD hh:mm:ss, which can
                            be changed via command line options, discussed with
                            examples in WWLOGGER.pdf, which is also included.
                            The time stamp is always followed by a single space,
                            then the message, which has no pre-set length limit.

                            Additional lines can be appended to the message by
                            writing them into a text file, then piping the text
                            to standard input by way of redirection characters.

WWLOGGERD.EXE               This is a Unicode version of WWLogger.exe; it works
                            identically, except that it outputs 16-bit Unicode
                            characters. Though the files created by the current
                            version lack a Byte Order Mark of any kind, I have
                            never had a problem reading them into a text editor
                            or spreadsheet program.

WWPause.exe                 I got fed up eons ago with batch files that took off
                            when ANY key was pressed, and wrote a DOS version of
                            this program. This is its 32 bit character mode son.

WWSleep.EXE                 This program allows a batch file to be suspended for
                            a user-defined number of seconds, with a default of
                            30 seconds if unspecified, to allow time for you to
                            read its output before the window in which it ran is
                            closed when the script exits.

ExportFromEventLogNDays.CMD This script uses the SysInternals PSLogList utility
                            to export records from a Windows event log. You must
                            supply your own copy of PSLogList.exe.

ShowArgs.BAT                This script displays the command line arguments of a
                            batch file. It can display up to nine arguments, but
                            it displays only actual arguments.

ShowTime.CMD                This script displays the current date and time, so a
                            script listing is time stamped.

XCOPYD.CMD                  This wrapper around stalwart system utility XCOPY is
                            the most dependable way I know to automatically give
                            the correct answer to the prompt about whether the
                            destination is a file or a directory when the answer
                            is that it is a directory.

XcopyDestIsDir.TXT          This response file answers the prompt from XCOPY.EXE
                            when the destination is a directory. XCOPYF.CMD
                            pipes it into XCOPY.EXE to automatically supply the
                            correct answer. This not only eliminate guesswork,
                            and a risk of responding incorrectly when using
                            XCOPY interactively in a command prompt window, but
                            it permits XCOPY to be run safely in unatteended
                            scripts, including build scripts, such as the one in
                            the Visual C++ build projects for my native DLLs.

                            This file and XCOPYD.CMD inhabit the same directory,
                            where XCOPYD.CMD parses its own fully qualified path
                            to work out where to find its response file.

XcopyDestIsFile.TXT         This is the response file for XCOPYF.CMD; it works
                            exactly like XcopyDestIsDir.TXT when the correct
                            response is that the destination is a file.

XCOPYF.CMD                  This wrapper around stalwart system utility XCOPY is
                            the most dependable way I know to automatically give
                            the correct answer to the prompt about whether the
                            destination is a file or a directory when the answer
                            is that it is a file.


The following table lists and briefly describes the dynamic-link libraries that
are included in the archive. Functions are listed alphabetically by name,
regardless of whether their type is Native or Managed.

------------
Native DLLs
------------

A DLL Type of Native denotes a DLL that is a Win32 dynamic link library that
exports its functions according to the __declspec(dllexport) calling convention,
and is suitable for use with any programming language that can call the Windows
API, including Visual Basic for Applications (VBA). Many of the functions return
pointers to strings, and have wrappers that return Basic Strings (BSTRs) that
are easier to use in VBA code, and are garbage collected. I have add-in modules
for Microsoft Excel that use many of these.

The Native DLLs are written almost entirely in C, and were built with a version
of the Microsoft Visual C++ compiler and tools. The older libraries were built
with Visual C++ 6.0, while the newest libraries were built with Visual C++ 12
(included with Visual Studio 2013). A handful of routines are implemented in
Assembler, and were assembled by the Microsoft Macro Assembler 6.11. All of them
run in the 32 bit subsystem on a 64 bit Windows machine.

------------
Managed DLLs
------------

A DLL type of Managed is a managed (Microsoft .NET) class library. All of the
libraries in this kit were built against version 2.0 of the framework, and are
compatible with that framework and all newer frameworks. They are implemented
exclusively in Visual C#, and most were built with Visual C# 2013. A few older
libraries were built with Visual C# 2010.

DLL Name                         DLL Type  Abstract
-------------------------------- --------- -------------------------------------
CreateFileWithRetry.dll          Native    This library exports one function,
                                           which is a drop-in replacement for
                                           the native CreateFile Win32 function.
                                           Like the routine it replaces, it has
                                           ANSI and wide character (Unicode)
                                           implementations.

FixedStringBuffers.dll           Native    This library exports wrappers around
                                           the Win32 LoadString function for
                                           loading Win32 resource strings and
                                           a set of static (baked in) buffers,
                                           for use with the printf family of
                                           formatted string printing functions.
                                           Other functions build on these to
                                           permit reporting appliation and
                                           system errors without the risk of the
                                           report failing due to low memory.

P6CStringLib1.dll                Native    This library exports numerous string
                                           parsing and manipulation functions.
                                           All functions have ANSI (narrow
                                           character), Unicode (wide character),
                                           and BSTR (Basic String) versions, and
                                           provide fast implementations of the
                                           string functions commonly provided by
                                           Basic and most scripting languages.

P6VersionInfo.dll                Native    This library exports a handful of
                                           convenience wrappers around the Win32
                                           version resource functions. There are
                                           ANSI and Unicode versions of all that
                                           return strings.

ProcessInfo.dll                  Native    This library exports a handful of
                                           specialized functions for obtaining
                                           information about the calling process
                                           such as the Windows subsystem in
                                           which it runs (Character or Windows)
                                           and the directory from which its main
                                           executable program loaded.

SafeMemCpy.dll                   Native    This library exports two functions
                                           (one ANSI and one Unicode) for safely
                                           copying strings into a buffer that
                                           was allocated from the process heap.
                                           Safe copying means that the buffer is
                                           expanded as needed to acommodate the
                                           copy.

WizardWrx.ApplicationHelpers.dll Managed   This class library exposes routines
                                           that maintain basic information about
                                           the main assembly under which they
                                           run, and for reporting exceptions,
                                           including optional recording in a
                                           Windows event log.

WizardWrx.ConsoleAppAids.dll     Managed   This class library exposes reoutines
                                           that cater to the needs of character
                                           mode (Console) programs, such as a
                                           robust command line argument parser.

WizardWrx.DateMath.dll           Managed   This class library exposes routines
                                           for manipulating and formatting dates
                                           and times.

WizardWrx.SharedUtl2.dll         Managed   This class library exposes a variety
                                           of classes that define commonly used
                                           numeric, Boolean, character, and
                                           string constants, and provide helper
                                           classes and methods for working with
                                           blocks of text, regular expressions,
                                           delimited lists, file names, and
                                           message digests.

WWConAid.dll                     Native    This library exports functions that
                                           cater to the needs of character mode
                                           (console) programs, such as routines
                                           for parsing "here" documents read
                                           from the standard input stream, and a
                                           little routine that halts a program
                                           until a carbon unit (you) presses the
                                           Enter (Return) key, displaying a
                                           default or custom message, and
                                           emitting a customizable beep through
                                           the built-in PC speaker to call
                                           itself to your attention.

WWDateLib.dll                    Native    This library exports functions that
                                           support extremely robust date formats
                                           and routines that determine correctly
                                           whether a given year is a leap year.

WWKernelLibWrapper.dll           Native    This library exports routines that
                                           allocate, reallocate, and deallocate
                                           blocks of memory from the default
                                           process heap. These routines use the
                                           Windows heap management functions,
                                           rather than the CRT functions (such
                                           as malloc, calloc, realloc, and free)
                                           because the CRT functions just wrap
                                           the same Windows functions and use a
                                           dedicated heap over which you have no
                                           control. Moreover, these functions
                                           use Structured Exception Handling to
                                           ensure precise information about any
                                           memory allocation error that may
                                           happen.

                                           Other routines provide conveniences,
                                           such as easy access to the names of
                                           the current working directory and the
                                           user's temporary directory, the full
                                           name of the current program and that
                                           of its directory, and the version of
                                           Microsoft Windows on which the code
                                           is running.
================================================================================
