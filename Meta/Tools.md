The tools I use:
* PCSX-Redux (https://github.com/grumpycoders/pcsx-redux)
	* The most powerful PSX emulator for debugging, it is my main emulator for all-things debugging, and has simplified my workflow so much compared to what it was three years ago, when I had to use multiple emulators to get things working.
* HexEdit (https://hexed.it/)
	* Browser-based text editor. Can be cached locally for offline use. Simple and does the job.
* Sublime Text (https://www.sublimetext.com/)
	* Lightweight text editor, compared to many modern alternatives. Will pester you to get a license.
* bgrep (https://github.com/tmbinc/bgrep)
	* Search tool for byte strings. Must be compiled yourself (see [[Compiling bgrep]]).
* Mkpsxiso/dumpsxiso (https://github.com/Lameguy64/mkpsxiso)
	* Image maker/dumper pair. Does the job.
* PSX-MODE2 (https://www.romhacking.net/utilities/848/)
	* Can handle changes in the filesize when recompiling the image file. It's a part of the Uncensored hack's toolchain.
* Obsidian (https://obsidian.md/)
	* Note-taking tool.
* ImHex (https://github.com/WerWolv/ImHex)
	* More advanced hex editor.
* Python (https://www.python.org/)
	* The main scripting language I use. It's simple but powerful. 
* C
	* The C programming language may be old at this point, but it gives me less headaches when working with more advanced byte manipulation.
* Armips (https://github.com/Kingcom/armips)
	* Assembler for ARM and MIPS. The syntax is very powerful.
* Ghidra (https://github.com/NationalSecurityAgency/ghidra)
	* Needs the Ghidra PSX plugin (https://github.com/lab313ru/ghidra_psx_ldr)
	* Reverse-engineering tool straight from the NSA. Allows you to reverse engineer the C code of the game to some extent. Far from perfect, but does the job.
* No$psx (https://problemkaputt.de/psx.htm)
	* Used to be my go-to emulator for debugging the GPU. That functionality has now been supplanted by PCSX-Redux. I still use it to make save states for the VRAM Viewer.
* VRAM Viewer
	* Comes in two versions: SDL (https://github.com/romhack/PsxVram-SDL) and DotNet (https://github.com/romhack/PsxVram-DotNet)
	* The DotNet version appears to be more updated, but I still use the SDL version.
	* This tool needs a No$psx savestate.