# OpenFilesInVim
When opening a file on mac, I wanted to open it in vim by double clicking it, after a little digging I found a few scripts (https://apple.stackexchange.com/questions/444204/how-to-open-text-files-in-vim-iterm2-by-double-clicking-on-their-names-in-find, https://gist.github.com/napcs/2d8376e941133ccfad63e33bf1b1b60c), but neither of them worked perfectly for me. Here is the combination that works perfectly for me. 

## AppleScript code
```
on run {input, parameters}
	set filename to quoted form of POSIX path of input
	set cmd to "clear;cd `dirname " & filename & "`;nvim " & filename
	tell application "iTerm"
		if application "iTerm" is running then
			tell the current window
				create tab with default profile
				tell the current session
					write text cmd
				end tell
			end tell
		else 
			tell the current window
				tell the current session
					write text cmd
				end tell
			end tell
		end if
		activate
	end tell
end run
```

## Steps

1. Open Automator
2. Choose "New Document"
3. Locate "Run AppleScript" and double-click it
4. Paste the Applescript code into the box
5. Save as /Applications/TerminalVim.app
6. In Finder, select some file you want to open in Vim, e.g. a .rb file.
7. Hit ⌘I to open the “Get Info” window.
8. Under “Open with:”, choose TerminalVim.app. You may need to select “Other…” and then browse.
9. Hit the “Change All…” button and confirm.
