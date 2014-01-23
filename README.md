#vdwrap

A simple wrapper around Vimdiff for diffing directory hierarchies with `git
difftool --dir-diff`. It is a Zsh script, so you need that installed.

With `vdwrap` instead of launching `vimdiff` once per pair of files Git will
launch it only once and you will see each pair in its own tab.

##Configuration:

You can configure this as your Git difftool straight up, or you can use it only
in combination with `--dir-diff`. When used without `--dir-diff` it tries its
best to invoke `vimdiff` the same way `git difftool` would have done anyway. I
haven't noticed any problems but it is a bit hacky.

In any case, put `vdwrap` somewhere in your `$PATH` and run

    git config --global difftool.vdwrap.cmd 'vdwrap $LOCAL $REMOTE'

If you don't want to put it in your path you can either also run

    git config --global difftool.vdwrap.path '/full/path'

or define the difftool using the full path:

    git config --global difftool.vdwrap.cmd '/full/path/vdwrap $LOCAL $REMOTE'
    git config --global diff.tool vdwrap

If you want to keep Vimdiff as the standard difftool and use the wrapper only
with `--dir-diff` you can define an alias, e.g.:

    git config --global alias.dirdiff 'difftool --tool vdwrap --dir-diff'

##Usage:

If you configure `vdwrap` as your difftool you do:
	
    git difftool --dir-diff foo bar
    git difftool foo bar

The latter should work just like normal.

Alternatively, using the alias:

    git dirdiff foo bar
    git difftool foo bar

Since `difftool --dir-diff` is long-winded you may want to define an alias
anyway, so it makes sense to not use `vdwrap` as your standard difftool.
