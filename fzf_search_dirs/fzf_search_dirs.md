# Configuring FZF to search useful directories beyond the working directory
<div style="text-align: justify">
<p>I use <a href="https://github.com/junegunn/fzf">fzf</a> both as a command
line tool and from within Vim using the <a
href="https://github.com/junegunn/fzf.vim">fzf.vim</a> plugin. It makes finding
(and opening) files intuitive, fast, and frees you from needing to remember
their location or exact name. By default, fzf searches recursively within the
current directory, which is often just what you want. If you need to search for
a file in some directory beyond the current working directory you need to
specify that path as an argument to fzf, after which it's business as usual
(fzf will recursively search the specified directory).</p> 
</div>

## The Problem
<div style="text-align: justify">
<p>It always felt a shame to have to occasionally precisely specify a path in
order to get a fuzzy search going... precisely specifying a path is the exact
thing that fzf is supposed to unburden your from! My initial approach was to
supply the home directory path and let fzf search everything, the home
directory path can be specified in only a couple of characters so there's no
real burden in that case.</p>

<p>The problem with doing this is that you end up searching a lot of
directories which you know don't have the file you want. The main offenders
were directories you end up with if you install say, anaconda3. The results
would be swamped with thousands of internal files, with very long paths. The
long paths tended to 'soak up' any letters I entered in the search, so it was
difficult for fzf to filter them out.</p>
</div>

## The Solution
<div style="text-align: justify">
<p>You can choose which searching tool fzf uses under the hood. The default is
the standard linux find command, but you can also use <a
href="https://github.com/sharkdp/fd#benchmark">fd</a>, ripgrep or silver
searcher. Apart from being a lot faster than the default find, these latter
tools <i>respect .gitignore files</i>. This means that fzf will skip any files
<b>or directories</b> listed in a .gitignore file. We can turn this feature to
our advantage.</p>

<p>First, we install <a href="https://github.com/sharkdp/fd#benchmark">fd</a>.
If you run Ubuntu 19.04 (Disco Dingo) or newer, you can install the officially
maintained package:</p>
</div>

{% highlight bash %}
sudo apt install fd-find
{% endhighlight %}

<div style="text-align: justify">
<p>If you use an older version of Ubuntu, you can download the latest .deb
package from the <a href="https://github.com/sharkdp/fd/releases">release
page</a> and install it via:</p>
</div>

{% highlight bash %}
# adapt version number and architecture
sudo dpkg -i fd_8.2.1_amd64.deb
{% endhighlight %}

<div style="text-align: justify">
<p>Now we configure fzf to use fd by adding the following line in your
.bashrc:</p>
</div>

{% highlight bash %}
export FZF_DEFAULT_COMMAND="fdfind . $HOME"
{% endhighlight %}

<div style="text-align: justify">
<p>If you're using an older version than Ubuntu 19.10, the above line needs to
be modified like so:</p>
</div>

{% highlight bash %}
export FZF_DEFAULT_COMMAND="fd . $HOME"
{% endhighlight %}

<div style="text-align: justify">
<p>Now fzf will always search recursively from the home directory, and respect
any .gitignore files in any git repository. fzf detects git repositories by
looking for a .git directory. We can trigger this behaviour in our home
directory by making a .git directory. To achieve this, your home directory must
not already be a git repository, but I don't think anyone does that... Then we
can create a .gitignore file to ignore any directories that we want - i.e the
ones swamping our searches:</p>
</div>

{% highlight bash %}
cd ~/
mkdir .git
touch .gitignore
{% endhighlight %}

<div style="text-align: justify">
<p>I find that the list of directories that I might conceivably (~15) want to
recursively search with fzf is shorter that the list of directories that I
would never want searched. The total number of files in the directories I want
searched is about 5000 or so - easily handled by fd.</p>

<p>In the .gitignore file, I first list all my home directories, each
followed by a '/':</p>
</div>

{% highlight bash %}
# start by igoring every home directory
anaconda3/
arch/
cache/
code/
Desktop/
  .
  .
  .
{% endhighlight %}

<div style="text-align: justify">
<p>Then <i>below</i> those, put the directories that you want to be searched, each
preceded by a '!' and followed by a '/':</p>
</div>

{% highlight bash %}
# now un-ignore the ones I care about
!code/
!Desktop/
!documents/
!downloads/
  .
  .
  .
{% endhighlight %}

<div style="text-align: justify">
<p>The '!' will 'cancel out' the previous ignore commands.</p>

<p>And there we have it. We can invoke fzf wherever we are in the file system
and start typing vague things about the file(s) we have in mind and fzf will
search in a set of predefined directories and find it with ease. This
completely removes the barrier of thinking where a file might be and how
precisely it was named.</p>

<div style="text-align: justify">
<p>N.B. I have noticed that, for some reason, a couple of subdirectories were
not showing up in the fzf search, and so I explicitly created some
'!path/to/missed/directory/' lines in this section...</p>

<p>N.B. You may be wondering "What if I find myself in an usual directory not
on the list, and want to use fzf?". I had the same concern so I put a couple of
aliases in my .bashrc that can toggle the above configuration on and off at
will (be sure to use 'fdfind' for Ubuntu 19.10+, as disused above):</p>
</div>

{% highlight bash %}
# restore fzf default options ('fzf clear')
alias fzfcl="export FZF_DEFAULT_COMMAND='fd .'"

# reinstate fzf custom options ('fzf-' as in 'cd -' as in 'back to where I was')
alias fzf-="export FZF_DEFAULT_COMMAND='fd . $HOME'"
{% endhighlight %}

<p>If you're using Vim to create the .gitignore file, an easy way to get a list
of all the directories in your home directory is the following command:</p>
</div>

{% highlight bash %}
:.!ls ~/
{% endhighlight %}

<div style="text-align: justify">
<p>Append a '/' to all lines by putting the cursor on the first directory in
the list and entering the following command:</p>
</div>

{% highlight bash %}
:.,$ norm A/
{% endhighlight %}

<div style="text-align: justify">
<p>Similar to above, insert the '!' before each one by putting the cursor on
the first directory in the list and entering the following command:</p>
</div>

{% highlight bash %}
:.,$ norm I!
{% endhighlight %}

<div style="text-align: right">
<a href="https://matt-a-bennett.github.io/fzf_launcher/fzf_launcher.html">Using FZF to select files for any program or command ></a>
</div>


[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/fzf_search_dirs/fzf_search_dirs.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

