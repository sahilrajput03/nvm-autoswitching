# README

For creating a working version of `.nvmrc` file -

```bash
node -v > .nvmrc
```

FYI: You can simply write 12 or 14 for corresonding node versions as well as I have done in this current demo.

## What to do to make autoswitching seamlessly?

In your `.bashrc` file you can have something like below and then autoswitching of node versions will happen quite amazingly!

```bash
nvmUse () {
	if [ -f ".nvmrc" ]; then
		nvm use
	fi
}

function cd {
    # actually change the directory with all args passed to the function
    builtin cd "$@"

	nvmUse
}
```
