# README

NVM Docs: [Docs](https://github.com/nvm-sh/nvm)

Inspiration: [here](https://stackoverflow.com/questions/57110542/how-to-write-a-nvmrc-file-which-automatically-change-node-version)

## Commands

```bash
# Install latest node version
nvm install node


# Insatll node LTS (Long-term Support)
nvm install --lts

# List of installed node versions
nvm list

# Some node versions I use
# 22.13.0
# 20.12.0
# 16.14.2



# Set default version of nvm
nvm alias default v22.13.0	# 14 Jan 2025 (latest - using this on macos)
# nvm alias default 20.12.0	# (older)


## Creating a `.nvmrc` file
node -v > .nvmrc

## ❤️ Switch to node version as mentioned in .nvmrc file in current working directory
nvm use

# Use defautl node version set in nvm (`check by nvm list | grep default`) in the current shell session
nvm use default
```

FYI: You can simply write 12 or 14 for corresonding node versions as well as I have done in this current demo.

## What to do to make autoswitching seamlessly?

*Note: [Official documentation of NVM](https://github.com/nvm-sh/nvm#calling-nvm-use-automatically-in-a-directory-with-a-nvmrc-file) also says about how to do this but the code they provided for `.zshrc` (`.bashrc`) didn't work in my macos as of 14 Jan 2025.*

In your `.bashrc` (or `~/.zshrc` [tested]) file you can add a statement `include ~/.bash_nvm`. *[Note: include is a my custom bash function that allows safe sourceing i.e, only source if file exists]*

And put below code in `~/.bash_nvm`:

```bash
nvmUse () {
	if [ -f ".nvmrc" ]; then
		nvm use
	fi
}
nvmUse
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
