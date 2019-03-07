# Information
Here's the stackoverflow question that started this whole project: 
https://stackoverflow.com/questions/3058325/what-is-the-difference-between-ps1-and-prompt-command

The file `prompt.sh` has the basic setup for adding this into your bashrc.
Basically, you make a function that sets `PS1` to a script, and call that
function from `PROMPT_COMMAND`, which will run whatever command you specify
each time you display `PS1`. 

Additional themes should be placed in the base/themes folder. The included
themes place all used scripts inside the base/bin folder, and locally set the
PATH to include it. Also, the included themes will NOT have a .sh extension,
while all additional scripts that are used WILL have the .sh extension.

To change themes from the command line:

`$ PROMPT_THEME="theme name"`

ex.

`$ PROMPT_THEME=twoline`

# Installation
Remove (or comment out) all `PS1` and `PROMPT_COMMAND` configuration from your
bashrc, and add the following line:

```
. [path_to_prompt.sh]
```

It will source the `prompt.sh` file, which exports some default variables
needed for the themes to work, and has the functions set up to use
`PROMPT_COMMAND` with whatever theme you choose (also some other goodies).

You could also just copy the section below and paste it into your `.bashrc` for
the basic functionality.

```
# Default prompt theme
export PROMPT_THEME="default"

# Path of base directory (used in theme scripts to find bin folder)
export PROMPT_BASE_DIR="$HOME/bin/bash_prompt"

function prompt_command {
    RET="$?"
    PS1=$("$PROMPT_BASE_DIR"/themes/"$PROMPT_THEME" "$RET")
}

PROMPT_COMMAND=prompt_command
```

The included themes take the return value of the last command as the only
parameter, but of course it doesn't need to be used. This just happens to be
the nicest way to do it.

You will need to change the variable `PROMPT_BASE_DIR` to the directory that
you cloned this repository. Additionally, the variable `PROMPT_THEME` sets the
default theme.
