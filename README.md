## BasicSynth Library

### BasicSynth version 1.5 - Release Notes

BasicSynth is a set of C++ libraries for sound generation and sequencing. 
The source distribution contains the source code to the libraries along with
numerous example programs and a complete multi-instrument synthesizer.

The ZIP file contains sources for all platforms. The CHM file is a 
Windows compiled help file for the library. This can be built from the
source distribution using doxygen.

BasicSynth Composer is a complete synthesis system based on the BasicSynth
sound generation libraries.

This release is focused on bug fixes, unicode support, and improving the 
build scripts.

1. Bug fixes
1.1 SoundFont playback
   Fixed a problem that would cause a crash if the MIDI modulation wheel
   is applied to the vibrato LFO.
1.2 Project files not loading float values
   Floating point values were not converted from strings due to locale settings.
1.3 Mixer configuration crash.
1.4 wxWidgets version of BSynthComposer
  This release fixes a variety of problems with BSynthCompserWX. This is
  still relatively new code, but is stable enough for use now. Also,
  the editor for Notelist now uses the "styled text control" (a/k/a scintilla).

2. Project files and Makefiles
2.1 Some VS project files would not build 64-bit versions.
  Paths and compiler settings were corrected.
2.2 Makefiles
  The makefiles have been modified so that the same
  file works for Linux and mingw on Windows. On Windows,
  run make from the msys shell.
2.3 Code::Blocks projects
  These have been modified to assume wxWidgets on Windows
  is built with mingw running under the msys shell.

 3. Unicode support
 3.1 Project files
  The project files now correctly output UTF-8 characters. This may
  cause some compatibility problems with prior versions. Prior versions
  marked the project files with encoding=UTF-8 but did not correctly 
  convert the text. Any non-ascii text in the project file will need to
  be corrected by bringing up the associtated properties dialog and
  reentering the values.
 3.2. BSynthComposer
  The mswin BSynthComposer supports display and entry of Unicode
  characters. Text files (e.g. Notelist) are assumed to be UTF-8.
  Notelist scores can now contain unicode characters in variable names,
  comments, and text strings.
 
 4. The FLTK version of BSynthComposer
  This is now deprecated since the wxWidgets version provides a 
  portable version that is easier to maintain with a better UI.
  The code is still included, but will not be updated or fixed.

### Contents

The _BasicSynth_ source is provided to support the book _BasicSynth: Creating a Music Synthesizer in Software_. (see [http://basicsynth.com](http://basicsynth.com).) The book provides detailed explanations of the signal processing functions required to generate and process sounds, and shows the derivation of the programs using the C++ language. Although the book is not required to use and understand the source, it should be read first if you do not have any experience with signal processing programming.

The _BasicSynth_ source distribution contains the following parts.

*   Common library - signal generation and processing library.
*   Instruments library - various synthesis instruments.
*   Notelist - a text-based music score language.
*   Examples and utilities - working programs that use the libraries.
*   BSynthComposer - a complete software synthesis program.

### Common library

The _BasicSynth_ Common library provides the signal generation and processing foundation for a software synthesizer. Much of the implementation is contained in the header files located in the Include directory. The file _BasicSynth.h_ includes all of the header files, or individual files can be included as needed. The methods are typically short, and placing them in the header allows the compiler to optimally expand the code as inline functions. Longer functions, and those that are not time critical, are located in the Src/Common directory and compiled into the Common library as object modules.

To build your own synthesis program with _BasicSynth_ you need at a minimum the Include files and the Common library (_Lib/Common.lib_). The Include directory and the Common library provide the sound generation, wave file and sequencer code. The header file _BasicSynth.h_ includes all of the library.

Note: Libraries for GCC (including MINGW) have the _.a_ extension instead of _.lib_

### Instruments

A set of example instruments built using the library are located in Src/Instruments. The instruments are intended for use with BSynthComposer (see below) but can also be used for other software synthesis systems.

If you want to use the _BasicSynth_ instruments collection in your program, you must also include the header file _Src/Instruments/Instruments.h_ and link the _Lib/Instruments.lib_ library.

### Notelist

Notelist is a musician friendly, text-based music score format. It allows simple representation of notes, and also includes programming functions to calculate note values. Notelist allows specifying synthesis parameters on a note-by-note basis. This provides complete control of the sound, not simply note-on and note-off specification.

To include the Notelist score processor in your program, you must include the header file _NLConvert.h_ from the _Src/Notelist_ directory and link the _Lib/Notelist.lib_ library.

### Examples

The source distribution includes numerous example programs that show usage of the library. The exmple programs are executed from the command line and are portable to many platforms. Some examples are under the directory Src/Utilties. These are specific to MS-WINDOWS.

### BasicSynth Composer

The BasicSynth source is intended to provide examples to someone who wants to create a personalized software synthesizer, and should not be treated as a completed synthesis project. However, a complete synthesizer (BSynthComposer) designed by the author for his own use is also included. This can be compiled and run as-is, but is also intended as a reference for how the BasicSynth libraries can be used as the foundation for your own synthesizer.

Three versions of BSynthComposer are available.

*   Windows - uses WTL for the GUI framework, GDI+ for graphics, DirectSound for audio.
*   FLTK - uses the FLTK for the GUI framework.
*   WX - uses wxWidgets for the GUI framework.

The MSWIN version only compiles with Visual Studio and only runs on Windows. The FLTK and WX versions can be compiled with the GNU or MinGW compilers and will run on Windows or Linux.

Several compositions for BSynthComposer are located in the ExampleProjects directory.

### Documentation

Reference documentation on the libraries is built with Doxygen. Use the files in the _Doxygen_ directory to build the documentation .html files. In addition, documentation in Windows help file format can be downloaded from the BasicSynth project on sourceforge.

* * *

## _BasicSynth_ Directory Structure

The BasicSynth directory structure is shown in the following diagram.

![](https://raw.githubusercontent.com/ffagerholm/basicsynth/master/Documents/Structure.jpg)


| Directory               | Usage                     |
|-------------------------|---------------------------|
| Bin                     | Executable images         |
| Lib                     | Object file libraries     |
| Binx64                  | 64-bit Executable images  |
| Libx64                  | 64-bit Object file libraries
| Include                 | Source include files. Much of the _BasicSynth_ sound generation code is contained in these files as inline class functions. |
| Documents               | Various documents.
| Doxygen                 | Configuration files to produce source code documentation with Doxygen. |
| OpenSource              | Open source libraries and include files. These are only used to build BSynthComposer. These are not needed to build the libraries and examples. However, the Windows examples (utilities) require WTL 8.0. |
| OpenSource/scintilla    | Header files and VS 2008 project files to build scintilla for BasicSynth. By default, the BSynthComposer looks here for the header files. If scintilla is installed already, change the project file for BSynthComposer to reference the include directory. |
| OpenSource/WTL80        | WTL files used by BasicSynth. By default, the BSynthComposer looks here for the header files. If WTL is installed already, change the project file for BSynthComposer to reference the include directory.
| OpenSource/fltk-*       | FLTK files used for BSynthCompser. These are not needed to build the libraries and examples. BSynthComposer can be built with either version 1.1.10 or 1.3.x. Version 1.3 is preferred. Later versions may work, but have not been tested. For Linux, the Makefiles use fltk-config to get the path to the FLTK include and library files. On Windows, the BSynthComposer FLTK project looks here for the header files and libraries. If FLTK is installed elsewhere, change the properties file for BSynthComposer to reference the appropriate directory. |
| OpenSource/wxWidgets-*  | wxWidget files used for BSynthCompser. These are not needed to build the libraries and examples. BSynthComposer can be built with either version 2.8.11 or 2.9.1. Other versions may work, but have not been tested. Version 2.9 is preferred. For Linux, the Makefiles use wx-config to get the path to the wxWidgets include and library files. On Windows, the BSynthComposer wx project looks here for the header files and libraries. If wxWidgets is installed elsewhere, change the properties file for BSynthComposer to reference the appropriate directory. |
| Src                     | Source code
| Src/Common              | Common library source. Implementation that is not contained in header files. Includes implementation of sequencers, audio, and generic file I/O |
| Src/Instruments         | Source to the _BasicSynth_ instruments collection library. |
| Src/Notelist            | Source to the notelist parser and interpreter library. |
| Src/Examples            | Source to the example programs. Each sub-directory contains one example program. The theory and algorithm of each program is explained in the associated book chapter. |
| Src/Utilities           | Source to the utility programs. Each sub-directory contains one utility program. These are Windows-only GUI programs that use the _BasicSynth_ library and demonstrate various synthesis techniques. |
| Src/BSynth              | Command line version of the synthesizer. |
| Src/GMSynth             | Plug-in synthesizer DLL using MIDI and SF2/DLS files. | 
| Src/BSynthComposer      | GUI version of the synthesizer. |
| Src/BSynthComposer/Core | Platform independent parts. |
| Src/BSynthComposer/mswin | MS-Windows specific code. |
| Src/BSynthComposer/Forms | XML files defining editor forms. | 
| Src/BSynthComposer/Help | Help files in HTML format and compiled help project for MS-Windows. |
| Src/BSynthComposer/fltk | FLTK specific code. |
| Src/BSynthComposer/wx | wxWidgets specific code. |

* * *

## Building _BasicSynth_

The author's target development environment for _BasicSynth_ is Windows using Visual Studio 2008. Consequently, the build procedure receives much more use and testing on Windows than other environments. Compiling with makefiles or Code:Blocks, GNU C++, MINGW, and building for Linux, may require some adjustments to make them work correctly on your computer.

* * *

### Building on MS-Windows with Visual Studio

There are several solution files that can be built depending on what you want to do. Default solution files are for Visual Studio 2008 (i.e. version 9). Solution files with 2005 in the name are for VisualStudio 2005 (version 8). Visual Studio 6 project files (.dsp) are also included. However, the older project files are not always kept up to date and you may need to modify them to produce working versions on the latest code. The VirtualKBD utility and BSynthComposer will not build with version 6 as they need the gdi+ libraries. If you have a different version of the compiler, you will have to produce the project and/or solution files from one of the supplied versions. Visual C++ Express edition will build most of BasicSynth without problems. However, to build BSynthComposer, and the Utilities, you need ATL. ATL is not included with VC Express, but may be available in the Platform SDK.

Each Visual Studio project defines four targets:

1.  Release Win32 - 32-bit version without debug info.
2.  Debug Win32 - 32-bit version with debugging.
3.  Release x64 - 64-bit version without debug info.
4.  Debug x64 - 64-bit version with debug info.

Output of the 32-bit release version is in Bin and Lib. The 64-bit version produces output in Bin64 and Lib64

To build everything, use the solution file _Src/BasicSynth.sln_

To build just the libraries, use the solution files in _Src/Common, Src/Instruments, and Src/Notelist_ directories.

To build the Example programs, use the solution file in _Src/Examples_. This builds all the example programs and libraries.

To build the utilities, use the solution file in _Src/Utilities_.

To build the stand-alone command line synthesizer, build the project in _Src/BSynth_.

To build the GUI synthesizer, build the project in Src/BSynthComposer

The utility programs and VC version of _BSynthComposer_ use WTL 8.0, available on sourceforge.net. The parts used by _BasicSynth_ are located in the _OpenSource/WTL80_ directory. _BSynthComposer_ requires the _scintilla_ header files and library DLL, also available on sourceforge.net. The parts used by _BasicSynth_ are located in the _OpenSource/scintilla_ directory. Pre-built DLLs are installed in the _Bin_ and _Binx64_ directories.

The fltk version of _BSynthComposer_ requires the FLTK header and library files. Source code is available from the [FLTK website.](http://www.fltk.org)

The wx version of _BSynthComposer_ requires the wxWidgets header and library files. Source code is available from the [wxWidgets website.](http://www.wxwidgets.org) Use the 2.9.x version. To build wxWidgets, use the appropriate solution file in wxWidgets\build\msw directory. The BasicSynth projects use a properties file (BSynthComposer\wx.props) to set the path to the wxWidgets directory. The default is _basicsynth\OpenSource\wxWidgets-2.9.3_.

* * *

### Building with Code::Blocks

There are two Code::Blocks workspace files for BasicSynth. In the Src directory, the basicsynth.workspace file will build the libraries and example programs. In the Src/BSynthComposer directory the BSynthComposer.workspace file will build the synthesizer program using either FLTK or wxWidgets.

The Code::Blocks installer for Windows includes a version of MinGW32. However, you should not use that version as it does not include the gdi+ libraries. Download and install the latest MinGW tools and then change the path to the compiler in Code::Blocks to reference the MinGW\bin directory. If you already have MinGW, check the include directory to insure that you have the gdiplus header files.

Projects contain four targets:

1.  Release Win32 - 32-bit Windows version without debug info.
2.  Debug Win32 - 32-bit Windows version with debugging.
3.  Release UNIX - Linux version without debug info.
4.  Debug UNIX - Linux with debug info.

There is a .cbp project file for each of the libraries, example programs, FLTK and wx versions of BasicSynth Composer. (The Utilities and MSWIN version of BasicSynth Composer use ATL and must be compiled with VisualStudio, so no .cbp files are provided.)

A global variable _bshome_ defines the location of include and library files. The first time you build the basicsynth workspace, Code::Blocks will prompt for the needed value. You can also set this in advance from the _Settings:Global Variables_ menu. The bshome value is the top directory where BasicSynth is installed (the _basicsynth_ directory). It's best to put the source in a path without spaces since the MINGW compiler and linker will have problems otherwise. However, if the path has spaces in it, there are ways around the problem. For Windows, you can create a network share name for the root folder and use the UNC path to access it. (e.g. \\MYCOMPUTER\BasicSynth).

When compiling on Linux the projects use the appropriate config file to determine the path for include and library files for wxWidgets and FLTK. When compiling on Windows you must set a variable for the path.

* * *

### Building with Makefiles

There is a master Makefile located in the Src directory. This will build the libraries and example programs. There is also a Makefile in each directory that can be used if you only want to build part of the system.

The file _BasicSynth.cfg_ in the Src directory contains the settings for the compiler and linker. Edit BasicSynth.cfg to point to the appropriate places. Usually you will only need to change the location of BSDIR in case you put the source in a directory other than your home directory. By default, BasicSynth is built with XML support using the tinyxml code in the Common directory. If you want to build with libxml2, you must install the libxml2-dev package and set the value in the BasicSynth.cfg file first before building BasicSynth. If you do not need to use the project/instrument file loading code, there is a null implementation of the XmlWrapper class that can be used instead. The file is Src/Common/XmlWrapN.cpp.

Output is to the directories Bin and Lib under the BasicSynth install directory. (Note the capitalization!)

There is a Makefile in _BSynthComposer_ that will build the FLTK and wx versions of BasicSynth Composer. There are install targets, installwx and installfltk, to install the binaries. You must _su_ to root for the install make.

> Note: I have noticed a problem with the GNU make that causes make to halt when descending three directory levels. Running make with the command line argument _--no-print-directory_ fixes this.

* * *

### Building with MINGW

The makefiles will work with MINGW if you also install MSYS. However, a different configuration file is used for mingw on Windows. Copy BasicSynth.mingw to BasicSynth.cfg before running make.

Compiling BSynthComposer with mingw presents some difficulties. To get high quality graphics, BSynthComposer for wxWidgets uses the GDI+ library, but this is not included with MINGW. It is possible to compile without GDI+, however. Set wxUSE_GRAPHICS_CONTEXT=0 when building wxWidgets to avoid this problem. Alternatively, you can get the GDI+ header files from the Windows SDK, edit them to work with mingw, then create an import file (libgdiplus.a) to reference the GDI+ dll.

When compiling the FLTK version of BSynthComposer, you will also need a regex library. Source to regex is included under the OpenSource directory. Compile the library and then copy to the MINGW library directory if needed.

* * *

## Example Programs

### Example01 (Chapter 5)

This example program shows a basic oscillator. It produces one second of a sin wave and writes the sound into the file Example01.wav

### Example02 (Chapter 6)

These examples demonstrate envelope generators. Example02 has in-line code, Example02a uses the BasicSynth Library, Example02b uses a graphics line algorithm.

### Example03 (Chapter 7)

Program to calculate complex waveforms.

*   summation of first 8 partials
*   sawtooth wave
*   inverse sawtooth wave
*   triangle wave
*   square wave
*   25% pulse wave
*   frequency modulation
*   phase modulation
*   amplitude modulation
*   ring modulation
*   white noise

### Example04 (Chapter 8)

Program to calculate complex waveforms using wavetable oscillators.

### Example4a

Program to dump the contents of SF2 and DLS files. When used with one of the -d options, a text dump of the file is produced. Otherwise, a WAV file of one or more samples is produced.

`example4a soundfont -bbank -ppreset -m -d(1|2|3) -wprefix -l[0|1] -n[0|1]`

| Option     | Use                                                    |
|------------|--------------------------------------------------------|
| `-d1`      | print internal representation used by BasicSynth       |
| `-d2`      | print raw file contents                                |
| `-d3`      | print both raw data and internal representation        |
| `-w_path_` | prefix to output file name                             |
| `-l0`      | don't preload samples                                  |
| `-l1`      | preload all samples (default)                          |
| `-bn`      | only output bank #n, else all banks                    |
| `-pn`      | only output patch #n, else all patches                 |

Bank numbers vary with the sound font file, but typically the sound font is a GM bank with melodic instruments in bank 0 and percussion instruments in bank 128. Additional melodic banks may exist as well.

### Example05 (Chapter 10)

Various filters, LP, HP, BP, Reson, using bi-quad filter; FIR and IIR averaging and convolution.

### Example06 (Chapter 9)

Program to demonstrate mixing and panning.

### Example07 (Chapter 11)

Using delay lines to implement echo.

### Example07a (Chapter 12)

Using delay lines to implement reverb.

### Examle07b (Chapter 13)

Using delay lines to implement Flanger/Chorus.

### Example08 (Chapter 15)

BasicSynth sequencer.

### Example09 (Chapter 16)

MIDI Sequencer.

### Example10 (Chapters 19-25)

Various Synthesizer Instruments.

`example10 [file]`

The _file_ parameter is the name of an XML file containing instrument definitions. See the documentation on the [instruments](Documents/Instruments.html) for the definition of the XML file format.

The _data.xml_ file contains definitions for the instruments to test.

*   Tone Generator
*   FM Tone Generator
*   Additive Synthesis
*   Subtractive Synthesis - variable waveform
*   Subtractive Synthesis - BUZZ generator
*   FM Synthesis (3 oscillators)
*   Matrix Synthesizer (8 oscillators, FM or Add)
*   Noise Sound Generator (Chuffer)
*   Wavefile Playback

* * *

## Utility Programs

The utility programs can be used to interactively explore various synthesis and signal processing techniques. These programs are built with Visual Studio on Windows and are not currently available in a portable version. The compiled files can be downloaded separately as a Windows .msi install file.

### Waveform Explorer

This program allows setting each of 16 partials to construct a complex waveform using the inverse Fourier transform (sum of sine waves). The resulting waveform can be saved to disk as a WAV file and as a graphic (EMF). Settings can be copied to the clipboard.

### FM Explorer

This program implements a three oscillator FM synthesizer. Each oscillator is combined with an ADSR envelope generator. Several presets are available as examples. The program can save the sound to a WAV file. The settings can also be copied to the clipboard.

### Reverb Explorer

This program implements a Schroeder reverb. The loop times and reverb time can be set from the program to hear how they affect the sound. Sounds can be internally generated or loaded from a WAV file. The processed sound can be saved to disk.

### Flanger Explorer

This program implements a Flanger/Chorus effect. The delay times, modulation depth, and amplitudes can be set to hear how they affect the sound. Sounds can be internally generated or loaded from a WAV file. The processed sound can be saved to disk.

### MIDI Player

This program uses the GMSynth DLL to produce a MIDI file playback program using either SoundFonts or DLS files to define instruments. A virtual keyboard allows playing the sounds interactively. MIDI keyboard input is also provided. Output can be sent directly to the sound card or to a WAV file.

* * *

## BSynth

This program is a complete synthesizer that runs from a command line. It takes one argument, the name of the project file to process.

BSynth _project.xml_

The [documentation on this program](Documents/BSynth.html) gives the specification for the project file and other related files.

* * *

## BSynthComposer

This program is a complete GUI synthesizer with mixer, wavetable editor, instrument editors, interactive playback using a virtual keyboard, MIDI keyboard input, and text score editor. The synthesizer can generate a WAV file or send output directly to the sound card. Three versions currently exist, a native Windows implementation, a portable implementation using FLTK, and a portable version using wxWidgets. On-line help and several example compositions are include to help get you started using the synthesizer.

* * *

©2008-2010, Daniel R. Mitchell, All rights reserved except as noted below.

See more synthesis stuff at [the _BasicSynth_ Website](http://basicsynth.com)

[<span style="text-decoration:none">![CC-GNU GPL](http://creativecommons.org/images/public/cc-GPL-a.png)</span>](http://creativecommons.org/licenses/GPL/2.0/)  
The source code to BasicSynth is © 2008-2011, Daniel R. Mitchell and is licensed under the [CC-GNU GPL](http://creativecommons.org/licenses/GPL/2.0/)Creative Commons/GNU-GPL. Source code may be used for non-commercial purposes without further restrictions.

Compositions in the ExampleProjects directory are © Daniel R. Mitchell and are licensed under the [Creative Commons Attribution-Noncommercial-No Derivitave Works license](http://creativecommons.org/licenses/by-nc-nd/3.0/us/).