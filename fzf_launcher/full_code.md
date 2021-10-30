# Full Code
Below is all the code that we have written to date.

[back to project main page](./fzf_launcher.md)\
[back to home](../index.md)

{% highlight bash %}

#!/bin/bash

# Run command/application and choose paths/files with fzf.
# Always return control of the terminal to user (e.g. when opening GUIs).
# The full command that was used will appear in your history just like any
# other (N.B. to achieve this I write the shell's active history to
# ~/.bash_history)
#
# Usage:
# f cd [OPTION]... (hit enter, choose path)
# f cat [OPTION]... (hit enter, choose files)
# f vim [OPTION]... (hit enter, choose files)
# f vlc [OPTION]... (hit enter, choose files)

f() {
    # if no arguments passed, just lauch fzf
    if [ $# -eq 0 ]
    then
        fzf | sort
        return 0
    fi

    # Store the program
    program="$1"

    # Remove first argument off the list
    shift

    # Store any option flags
    options="$@"

    # Store the arguments from fzf
    arguments=$(fzf --multi)

    # If no arguments passed (e.g. if Esc pressed), return to terminal
    if [ -z "${arguments}" ]; then
        return 1
    fi

    # Sanitise the command by putting single quotes around each argument, also
    # first put an extra single quote next to any pre-existing single quotes in
    # the raw argument. Put them all on one line.
    for arg in "${arguments[@]}"; do
        arguments=$(echo "$arg" | sed "s/'/''/g; s/.*/'&'/g; s/\n//g")
    done

    # If the program is on the GUI list, add a '&'
    if [[ "$program" =~ ^(nautilus|zathura|evince|vlc|eog|kolourpaint)$ ]]; then
        arguments="$arguments &"
    fi

    # Write the shell's active history to ~/.bash_history.
    history -w

    # Add the command with the sanitised arguments to .bash_history
    echo $program $options $arguments >> ~/.bash_history

    # Reload the ~/.bash_history into the shell's active history
    history -r

    # execute the last command in history
    fc -s -1
    }

{% endhighlight %}

[back to project main page](./fzf_launcher.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/fzf_launcher/full_code.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

