# Installation

Clone the repository from **GitLab**:

    $ git clone https://gitlab.com/seismic_imaging/rapidalignerseismic

Checkout the `motif_searching` branch:

    $ cd rapidalignerseismic
    $ git checkout motif_searching


Download the **singularity** container in the top directory of the repository.
The name of the container is `Container_rapid.simg`

Create a file called `singularity_bashrc` with the following contents:

```
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/usr/local/miniconda/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/usr/local/miniconda/etc/profile.d/conda.sh" ]; then
        . "/usr/local/miniconda/etc/profile.d/conda.sh"
    else
        export PATH="/usr/local/miniconda/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

These are the typical instructions added by **Anaconda** (or **Miniconda**)
to the user's `.bashrc` file to initialize the `conda` installer.




