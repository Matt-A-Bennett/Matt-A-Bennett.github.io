# Using FZF to select files for any program or command

The full code I've written so far can be found [here](./full_code.md).

<div style="text-align: justify">
<p>I use <a href="https://github.com/junegunn/fzf">fzf</a> all the time in the
terminal. One very useful feature is to search for and select files to be
passed to some command (e.g. cat) or program (e.g. vlc). This is especially
useful when fzf is configured to always search a set of default directories
scattered around the file system, described in the <a
href="../fzf_search_dirs/fzf_search_dirs.html">previous post</a>.</p>
</div>

## The Goal
<div style="text-align: justify">
<p>Here I create a bash function to automate this procedure. The function is
called with the command or program as an argument. The function launches fzf,
you select your file(s) and hit enter. The selected files are passed to the
command/program. Apart from being a little easier to type than 'vlc $(fzf)',
the function returns control of the terminal to the user (e.g. when opening
GUIs). The full command that was run after expansion will appear in your
history just like any other.</p>

<p>Here we open a couple of python files in vim (the two marked with red
circles), from two separate directories, and neither of which is in the current
working directory. Note how few characters is needed to locate the files with
fzf:</p>
</div>
![Loading multiple files in vim](./images/fzf_search_multi_demo.png)

<div style="text-align: justify">
<p>The command is found in our history in a way we could re-execute (note that
I wrapped the lines here so it would fit in the image, in reality the command
appears as a single line:</p>
</div>
![The history looks good](./images/fzf_multi_history.png)

<div style="text-align: justify">
<p>A really useful case is to change directory to somewhere far away in the
file system: </p>
</div>
![changing to a far away directory](./images/fzf_cd_demo.png)

<div style="text-align: justify">
<p>Again, the command is found in our history in a way we could re-execute:</p>
</div>
![The history looks good](./images/fzf_cd_history.png)

<div style="text-align: justify">
<p>The usage is like this:<br/>
f cd [OPTION]... (hit enter, choose path)<br/>
f cat [OPTION]... (hit enter, choose files)<br/>
f vim [OPTION]... (hit enter, choose files)<br/>
f vlc [OPTION]... (hit enter, choose files)</p>
</div>

## The Code Implementation
<div style="text-align: justify">
<p>The general method is to construct a command in ~/.bash_history taking the
form: program + options + arguments. We use fzf to supply the file names which
we'll use as arguments. Then we simply execute that command.</p>

<p>First we store the first argument as the program and shift it off the
argument list. Any remaining arguments are taken as options to the program,
which we pad with spaces. </p>

{% highlight bash %}

#!/bin/bash

f() {
    # Store the program
    program="$1"

    # Remove first argument off the list
    shift

    # Store any option flags with separating spaces
    options=" $@ "

{% endhighlight %}

<p>We launch fzf with the possibility of selecting multiple items and
collect the arguments and store them in a variable:</p>

{% highlight bash %}

# Store the arguments from fzf
arguments=$(fzf --multi)

# If no arguments passed (e.g. if Esc pressed), return to terminal
if [ -z "${arguments}" ]; then
    return 1
fi

{% endhighlight %}

<p>The command typed into the terminal could for example be 'f vlc'. The
function will expand that into 'vlc file1.mp3 file2.mp3 &' and we want
<i>that</i> command to show up in our bash history, rather than just seeing 'f
vlc'. So we first write the shell's active history to the ~/.bash_history file,
then later we'll add this 'vlc file1.mp3 file2.mp3 &' command to the end of
~/.bash_history. Once we're all done, we'll load the ~/.bash_history file as
our active history.</p> 

{% highlight bash %}

history -w

{% endhighlight %}

<p>Next we store the arguments passed to our program in a temporary variable
and sanitise them for entry into ~/.bash_history. Specifically, we use sed to
put all input arguments on one line wrap the command by single quotes each the
argument, also we put an extra single quote next to any pre-existing single
quotes in the raw argument (e.g. badly named files). This has the effect that
the quote in the argument itself is respected as such.</p>

{% highlight bash %}

    for arg in "${arguments[@]}"; do
        arguments=$(echo "$arg" | sed "s/'/''/g; s/.*/'&'/g; s/\n//g")
    done

{% endhighlight %}

<p>In general, we want to launch GUI programs as background jobs so that we can
still enter other commands into the terminal as they run. Non-GUI commands that
run in the terminal such as 'vim', 'cat', 'head' etc should be run as
foreground jobs (otherwise we won't see them). If the program is on the list of
GUI programs, we append '&' on the end of the command.</p> 

{% highlight bash %}

if [[ "$program" =~ ^(nautilus|zathura|evince|vlc|eog|kolourpaint)$ ]]; then
    arguments="$arguments &"
fi

{% endhighlight %}

<p>Now we just append the sanitised commands to the ~/.bash_history, then
reload the contents of the ~/.bash_history as our active history.</p>

{% highlight bash %}

echo $program$options$arguments >> ~/.bash_history

history -r

{% endhighlight %}

<p>Finally, we execute the command that we placed in ~/.bash_history:</p>

{% highlight bash %}

fc -s -1
}

{% endhighlight %}

</div>

The full code I've written so far can be found [here](./full_code.md).

[< Configuring FZF to search useful directories beyond the current working directory](../fzf_search_dirs/fzf_search_dirs.md)

[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/fzf_launcher/fzf_launcher.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

