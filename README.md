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

## what is `engine-strict=true` in `.npmrc` file (ChatGPT)

Setting `engine-strict=true` in Node.js enforces strict compatibility with the version specified in the engines field of your package.json file. Here’s how it works:

Purpose: By default, the engines field in package.json specifies compatible Node.js and npm versions, but it doesn't prevent installation if there's a version mismatch. However, if you set `engine-strict=true`, it will make these specifications mandatory, meaning npm will throw an error if the Node.js or npm version doesn't match the specified versions.

Use Case: This is useful for ensuring that your project is only run on compatible versions, reducing the risk of unexpected errors due to version differences.

How to Set It: You can add this flag in your `.npmrc` file like this:

`engine-strict=true`

Or, you can set it as a one-time configuration by running:

`npm config set engine-strict true`

When enabled, if a user tries to install or run the project with an incompatible Node.js version, npm will prevent the installation.
