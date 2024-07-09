# README

NVM: [Docs](https://github.com/nvm-sh/nvm)

Inspiration: [here](https://stackoverflow.com/questions/57110542/how-to-write-a-nvmrc-file-which-automatically-change-node-version)

## Install latest node version

```bash
nvm install node
```

## Set default version of nvm

```bash
nvm alias default 20.12.0
# Other versions 16.14.2, etc.
nvm use default
```

## Creating a `.nvmrc` file

```bash
node -v > .nvmrc
```

FYI: You can simply write 12 or 14 for corresonding node versions as well as I have done in this current demo.

**What to do to make autoswitching seamlessly?**

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
