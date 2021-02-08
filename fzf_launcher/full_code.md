# Full Code
Below is all the code that we have written to date.

[back to project main page](./fzf_launcher.md)\
[back to home](../README.md)

{% highlight bash %}

#!/bin/bash

# Run command/application and choose paths/files with fzf.
# Always return control of the terminal to user (e.g. when opening GUIs).
# The full command that was used will appear in your history just like any
# other (N.B. to achieve this I write the shell's active history to
# ~/.bash_history)
#
# Usage:
# f cd (hit enter, choose path)
# f cat (hit enter, choose files)
# f vim (hit enter, choose files)
# f vlc (hit enter, choose files)

f() {
    # Store the arguments from fzf
    IFS=$'\n' arguments=($(fzf --query="$2" --multi))

    # If no arguments passed (e.g. if Esc pressed), return to terminal
    if [ -z "${arguments}" ]; then
        return 1
    fi

    # We want the command to show up in our bash history, so write the shell's
    # active history to ~/.bash_history. Then we'll also add the command from
    # fzf, then we'll load it all back into the shell's active history
    history -w

    # RUN THE COMMANDS ########################################################
    # The cd command has no effect when run as background, and doesn't show up
    # as a job the can be brought to the foreground. So we make sure not to add
    # a '&' (more programs can be added separated by a '|')
    if ! [[ $1 =~ ^(cd)$ ]]; then
        $1 "${arguments[@]}" &
    else
        $1 "${arguments[@]}"
    fi

    # If the program is not on the list of GUIs (e.g. vim, cat, etc.) bring it
    # to foreground so we can see the output. Also put cd on this list
    # otherwise there will be errors)
    if ! [[ $1 =~ ^(cd|zathura|evince|vlc|eog|kolourpaint)$ ]]; then
        fg %%
    fi

    # ADD A REPEATABLE COMMAND TO THE BASH HISTORY ############################
    # Store the arguments in a temporary file for sanitising before being
    # entered into bash history
    : > /tmp/fzf_tmp
    for file in ${arguments[@]}; do
        echo $file >> /tmp/fzf_tmp
    done

    # Put all input arguments on one line and sanitise the command by putting
    # single quotes around each argument, also first put an extra single quote
    # next to any pre-existing single quotes in the raw argument
    sed -i "s/'/''/g; s/.*/'&'/g; s/\n//g" /tmp/fzf_tmp

    # If the program is on the GUI list add a '&' to the command history
    if [[ $1 =~ ^(zathura|evince|vlc|eog|kolourpaint)$ ]]; then
        sed -i '${s/$/ \&/}' /tmp/fzf_tmp
    fi

    # Grab the sanitised arguments
    arguments=$(cat /tmp/fzf_tmp)

    # Add the command with the sanitised arguments to our .bash_history
    echo ${1} ${arguments} >> ~/.bash_history

    # Reload the ~/.bash_history into the shell's active history
    history -r

    # Clean up temporary variables
    rm /tmp/fzf_tmp
}

{% endhighlight %}

[back to project main page](./fzf_launcher.md)\
[back to home](../README.md)

<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/fzf_launcher/full_code.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

