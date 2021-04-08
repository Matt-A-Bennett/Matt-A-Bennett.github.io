# One command to switch between light and dark mode in Vim and Tmux
<div style="text-align: justify">
<p>I always have one of my monitors taken up with Vim and/or Tmux as I work,
and have up until now used dark themes. Here I implement a way to switch from a
light to dark colour scheme for both Vim and Tmux in one with a simple shortcut
entered into either.</p>

<p>In my case I can do either:</p>

<p>
From a Tmux pane:
1a) The alias 'ol' switches <b>both</b> Vim and Tmux to light mode.
1b) The alias 'od' switches <b>both</b> Vim and Tmux to dark mode.
</p>

<p>
From Vim:
2) 'Leader-o' toggles <b>both</b> Vim and Tmux between light and dark colour
schemes.
</p>
</div>

![dark theme](./images/all_dark.png)
![light theme](./images/all_light.png)

<div style="text-align: justify">
<p>The way it works is that I define an Tmux environmental variable that keeps
track of whether we have a light or dark colour scheme. Anytime I switch, be it
from Vim of a Tmux pan, the variable will be updated. Existing and new Tmux
panes and existing and new instances of Vim will check this variable and follow
the scheme.
</p>
</div>

## Code implementation
### Step 1: Tmux
<div style="text-align: justify">
<p>First, I've configured my bashrc such that it will automatically launch Tmux
and attempt to connect to a session called 'main', or create it if it doesn't
exist. I find this works for me, but you may want to alter this step.</p>

<p>Once I've launch Tmux, I query the environment variable called 'THEME', if
it's not equal to 'THEME=light' (or just doesn't exist), then we go with the
dark theme. This means that when we first launch a Tmux session, we will
default to a dark theme.</p>
</div>

{% highlight bash %}
if command -v tmux>/dev/null; then
    [[ ! $TERM =~ screen ]] && [ -z $TMUX ] && tmux new-session -A -s main

    # check if we have been switched to light, else go dark
    [[ ! $(tmux show-environment | grep THEME) =~ 'THEME=light' ]] && 
    tmux set-environment THEME dark
fi
{% endhighlight %}

<div style="text-align: justify">
<p>At the beginning of my ~/tmux.conf file, I start by sourcing a secondary
Tmux file that contains the dark colours I've chosen. These values may get
overridden later.</p>
</div>

{% highlight bash %}
# source colorscheme
set -g default-terminal 'screen-256color'
source-file ~/.tmux_dark.conf
{% endhighlight %}

<div style="text-align: justify">
<p>This is the dark theme colours I have:</p>
</div>

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

<div style="text-align: justify">
<p>In addition to ~/.tmux_dark.conf, I have ~/.tmux_light.conf:</p>
</div>

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

<div style="text-align: justify">
<p>If I'm in a Tmux pane, and want to switch colour schemes, I just source the
relevant file, and update the THEME variable. I have two aliases in my
~/.bashrc to do this. I remember them as ol for 'ON/Light', and od for
'OFF/Dark':</p>
</div>

{% highlight vim %}
# switch between light and dark themes
alias ol="tmux source-file ~/.tmux_light.conf; tmux set-environment THEME 'light'"
alias od="tmux source-file ~/.tmux.conf; tmux set-environment THEME 'dark'"
{% endhighlight %}

### Step 2: Vim
<div style="text-align: justify">
<p>In my ~/.vimrc, I defined two functions, one to set the colour scheme and
another to handle the reading and updating of the Tmux THEME variable. The
colour scheme we pick is dictated by the Tmux THEME variable, which we read
with a system call to Tmux. This returns the  THEME variable, as well as a
message saying 'Press ENTER or type a command to continue'. Obviously we're
only interested in the variable. If the variable indicates we should be dark,
we choose a dark colour scheme (in my case zenburn), otherwise we go with a
light on (in my case seoul256-light).</p>
</div>

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

<div style="text-align: justify">
<p>If we are in Vim, and want to toggle the colour scheme between light and
dark, we do it with a function. The function also re-sources the appropriate
Tmux colour scheme and updates the THEME variable. Once the THEME variable is
updated, we call the SetColorScheme function above to change Vim's colours:</p>
</div>

{% highlight vim %}
function! Toggle_Light_Dark_Colorscheme()
    if system('tmux show-environment THEME')[0:9] != 'THEME=dark'
        :silent :!tmux source-file ~/.tmux.conf
        :silent :!tmux set-environment THEME 'dark'
    else
        :silent :!tmux source-file ~/.tmux_light.conf
        :silent :!tmux set-environment THEME 'light'
    endif
    :call SetColorScheme()
endfunction
{% endhighlight %}

<div style="text-align: justify">
<p>We can create a mapping (or a command) to quickly toggle the colour scheme
like so:</p>
</div>

{% highlight vim %}
    nnoremap <Leader>o :call Toggle_Light_Dark_Colorscheme()<cr>
{% endhighlight %}

<div style="text-align: justify">
<p>When we open a new instance of Vim, the Tmux THEME variable with already be
sent, and so we choose the colour scheme using the SetColorScheme function:</p>
</div>

{% highlight vim %}
call SetColorScheme()
{% endhighlight %}

<div style="text-align: justify">
<p>We could stop there, but in the case where we have a Vim open, and change
the scheme from one of our aliases from withing in a Tmux pane, Vim won't
automatically re-run the SetColorScheme function.</p>
</div>

![toggle in tmux, with vim open](./images/dark_to_light_tmux.png)

<div style="text-align: justify">
We can use an autocmd to
check reset the colour scheme when ever Vim is re-focuesed. Unfortunately, this
doesn't work for Vim in the terminal, but luckily there is a plugin that
resolves it for us:
</div>

{% highlight vim %}
Plugin 'tmux-plugins/vim-tmux-focus-events'
{% endhighlight %}

<div style="text-align: justify">
<p>This will mean that as soon as you return to vim from the Tmux pane, Vim's
colour scheme will update automatically.</p>
</div> 

{% highlight vim %}
    autocmd FocusGained * :call SetColorScheme()
{% endhighlight %}

![light theme](./images/all_light.png)


<div style="text-align: justify">
<p>It would probably be easy to coerce Vim to constantly check that the Tmux
THEME variable, but I only switch from light to dark in the evening (i.e. once
a day) so I don't want to make Vim do a million checks in the background for
such a rare event: </p>
</div>

<div style="text-align: justify">
<p>One last remark is that I opted to change the colour of my command prompt to
be visible under both colour schemes. In my ~/.bashrc I put 35m to specify a
purple colour in bold font. How these numbers specify a colour is mysterious to
me, so I just googled around a bit:</p>
</div>

{% highlight bash %}
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;35m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\n\$ '
{% endhighlight %}

<div style="text-align: justify">
<p>However, choosing colours in the ~/.tmux.conf file is easy with this which
can be pasted into the terminal to display a colour grid of the 0-255
range.</p>
</div>

{% highlight bash %}
for i in {0..255} ; do \
printf "\x1b[48;5;%sm%3d\e[0m " "$i" "$i"; \
if (( i == 15 )) || (( i > 15 )) && (( (i-15) % 6 == 0 )); then \
printf "\n"; \
fi; done
{% endhighlight %}

[back to home](../index.md)
