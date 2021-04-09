# Switch between light and dark mode in Vim and Tmux with one command 
<div style="text-align: justify">
<p>I always have one of my monitors taken up with Vim and/or Tmux as I work,
and have up until now used dark themes. Here I implement a way to toggle
between a light and dark colour scheme for both Vim and Tmux in one go with a
simple shortcut (entered into either Vim or a Tmux pane).</p>

<p>In my case I can do either:</p>

<p>From a Tmux pane:<br>
<b>1a)</b> The alias 'ol' switches <b>both</b> Vim and Tmux to light mode.<br>
<b>1b)</b> The alias 'od' switches <b>both</b> Vim and Tmux to dark mode.<br></p>

<p>From Vim:<br>
<b>2)</b> 'Leader-o' toggles <b>both</b> Vim and Tmux between light and dark colour
schemes.</p>
</div>

![dark theme](./images/all_dark.png)
![light theme](./images/all_light.png)

<div style="text-align: justify">
<p>The way it works is that I define a Tmux environmental variable that keeps
track of whether we have a light or dark colour scheme. Anytime I switch, be it
from Vim or a Tmux pane, the variable will be updated. Existing and new Tmux
panes and existing and new instances of Vim will check this variable and follow
the scheme.</p>
</div>

## Code implementation
### Step 1: Switching colours from inside a Tmux pane
<div style="text-align: justify">
<p>For the purpose of this guide, I'll assume my various dot files are in my
home directory. In reality I keep them all in a single git repository with
symbolic links from the home directory to allow me to keep my working
environment synchronised across machines as described on this <a
href="https://github.com/Matt-A-Bennett/linux_config_files">git repo</a>.</p>

<p>First, I've configured my ~/.bashrc such that it will automatically launch
Tmux and attempt to connect to a session called 'main', or create it if it
doesn't exist. I find this works for me, but you may want to alter this
step.</p>

<p>Once I've launched Tmux, I query the environment variable called 'THEME', if
it's not equal to 'THEME=light' (or just doesn't exist), then we go with the
dark theme and set the THEME variable accordingly. This means that when we
first launch a Tmux session, we will default to a dark theme:</p>

{% highlight bash %}
if command -v tmux>/dev/null; then
    [[ ! $TERM =~ screen ]] && [ -z $TMUX ] && tmux new-session -A -s main

    # check if we have been switched to light, else go dark
    [[ ! $(tmux show-environment | grep THEME) =~ 'THEME=light' ]] && 
    tmux set-environment THEME dark
fi
{% endhighlight %}

<p>At the beginning of my ~/tmux.conf file, I start by sourcing a secondary
Tmux file that contains the dark colours I've chosen. These values may get
overridden by a light scheme later:</p>

{% highlight bash %}
# source colorscheme
set -g default-terminal 'screen-256color'
source-file ~/.tmux_dark.conf
{% endhighlight %}

<p>These are the dark theme colours I have:</p>

{% highlight bash %}
# dark colours
# fg = thin line
set -g pane-border-style "bg=colour234 fg=colour244"
set -g pane-active-border-style "bg=colour234 fg=colour208"
# fg = text
set -g window-style 'fg=colour248,bg=colour234'
set -g window-active-style 'fg=colour252,bg=colour235'
# Customize the status line
set -g status-fg colour208
set -g status-bg colour234
{% endhighlight %}

<p>In addition to ~/.tmux_dark.conf, I have ~/.tmux_light.conf:</p>

{% highlight bash %}
# light colours
# fg = thin line
set -g pane-border-style "bg=colour253 fg=colour244"
set -g pane-active-border-style "bg=colour253 fg=colour208"
# fg = text
set -g window-style 'fg=colour238,bg=colour253'
set -g window-active-style 'fg=colour238,bg=colour231'
# Customize the status line
set -g status-fg colour208
set -g status-bg colour253
{% endhighlight %}

<p>If I'm in a Tmux pane, and want to switch colour schemes, I just source the
relevant file, and update the THEME variable. I have two aliases in my
~/.bashrc to do this. I remember them as ol for 'ON/Light', and od for
'OFF/Dark':</p>

{% highlight vim %}
# switch between light and dark themes
alias ol="tmux source-file ~/.tmux_light.conf; tmux set-environment THEME 'light'"
alias od="tmux source-file ~/.tmux_dark.conf; tmux set-environment THEME 'dark'"
{% endhighlight %}
</div>

### Step 2: Switching colours from inside Vim
<div style="text-align: justify">
<p>In my ~/.vimrc, I've defined two functions, the first handles the updating
of the Tmux THEME variable and toggles the Tmux colours, and the second sets
Vim's colours.</p>

<p>We read the Tmux THEME with a system call to Tmux. This returns the THEME
variable, as well as a message saying 'Press ENTER or type a command to
continue'. Obviously we're only interested in the variable. Importantly, since
I'm checking a match with 'THEME=dark', we must take only the first 10
characters of message returned by the system call. Whichever scheme the
variable indicates that we're using, we source the alternate theme and update
the THEME variable. Once the THEME variable is updated, we call the
SetColorScheme function above to change Vim's colours:</p>

{% highlight vim %}
function! Toggle_Light_Dark_Colorscheme()
    if system('tmux show-environment THEME')[0:9] == 'THEME=dark'
        :silent :!tmux set-environment THEME 'light'
        :silent :!tmux source-file ~/.tmux_light.conf
    else
        :silent :!tmux set-environment THEME 'dark'
        :silent :!tmux source-file ~/.tmux_dark.conf
    endif
    :call SetColorScheme()
endfunction
{% endhighlight %}

<p>The colour scheme we pick is dictated by the Tmux THEME variable. If the
THEME is 'THEME='dark', we choose a dark colour scheme (in my case zenburn),
otherwise we go with a light one (in my case seoul256-light):</p>

{% highlight vim %}
function! SetColorScheme()
    " check if tmux colorsheme is light or dark, and pick for vim accordingly
    if system('tmux show-environment THEME')[0:9] == 'THEME=dark'
        colorscheme zenburn
    else
        colorscheme seoul256-light
    endif
endfunction
{% endhighlight %}

<p>We can create a mapping (or a command) to quickly toggle the colour scheme
like so:</p>

{% highlight vim %}
nnoremap <Leader>o :call Toggle_Light_Dark_Colorscheme()<cr>
{% endhighlight %}

<p>When we open a new instance of Vim, the Tmux THEME variable will have
already been defined, and so we choose the colour scheme using the
SetColorScheme function (note that this must come after the SetColorScheme
function in your ~/.vimrc):</p>

{% highlight vim %}
call SetColorScheme()
{% endhighlight %}

<p>We could stop there, but in the case where we have an instance of Vim
running, and change the scheme using one of our aliases from within in a Tmux
pane, Vim won't automatically re-run the SetColorScheme function:</p>
</div>

![toggle in tmux, with vim open](./images/dark_to_light_tmux.png)

<div style="text-align: justify">
We can use an autocmd to check and reset the colour scheme whenever Vim is
re-focused. Unfortunately, this doesn't work for Vim in the terminal, but
luckily there is a <a
href="https://github.com/tmux-plugins/vim-tmux-focus-events">plugin </a> that
resolves it for us:

{% highlight vim %}
Plugin 'tmux-plugins/vim-tmux-focus-events'
{% endhighlight %}

<p>This plugin requires the following line in your ~/.tmux.conf (or that you've
installed the <a
href="https://github.com/tmux-plugins/tmux-sensible">tmux-sensible</a>
plugin):</p>

{% highlight bash %}
set -g focus-events on
{% endhighlight %}

<p>With one of the above options (I just have the line in my ~/.tmux.conf), we
can use the FocusGained event in ~/.vimrc:</p>

{% highlight vim %}
autocmd FocusGained * :call SetColorScheme()
{% endhighlight %}

<p>This will mean that as soon as you return to vim from the Tmux pane, Vim's
colour scheme will update automatically:</p>
</div> 

![light theme](./images/all_light.png)

<div style="text-align: justify">
<p>It would probably be easy to coerce Vim to constantly check the Tmux THEME
variable, but I only switch from light to dark in the evening (i.e. once a day)
so I don't want to make Vim do a million checks in the background for such a
rare event: </p>

<p>One last remark is that I opted to change the colour of my command prompt to
be visible under both colour schemes. In my ~/.bashrc I put 35m to specify a
purple colour in bold font. How these numbers specify a colour is mysterious to
me, so I just googled around a bit:</p>

{% highlight bash %}
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;35m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\n\$ '
{% endhighlight %}

<p>However, choosing colours in the ~/.tmux.conf file is easy with this code
which can be pasted into the terminal to display a colour grid of the 0-255
range:</p>

{% highlight bash %}
for i in {0..255} ; do \
printf "\x1b[48;5;%sm%3d\e[0m " "$i" "$i"; \
if (( i == 15 )) || (( i > 15 )) && (( (i-15) % 6 == 0 )); then \
printf "\n"; \
fi; done
{% endhighlight %}
</div>

[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/colour_switching_terminal/colour_switching_terminal.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

