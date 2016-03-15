# Montreal Python 57 presentation content

## Uncompressing the audio sample files

There are two archives of audio files, the training data `genres2` and the
additional data `lastfm-top-tracks`. Uncompress all archives with the provided
script:

    ./setup


## Installing the required packages

The list of Python packages necessary to run the code is specified in the `requirements.txt` file.
You can create a virtualenv to isolate the changes from your other projects, or install the
packages in "user" mode so that you can access them easily without affecting your global system
configuration. I choose the second option, which is simply prepared with a single command:

    pip3 install --user -r requirements.txt

Note that this may require some system packages to be available on your computer. For example, on
Ubuntu and Debian systems, you can get them with:

    apt-get install build-essential python3-dev libsamplerate0-dev libsndfile1-dev

If you install Jupyter in user mode, the command may not be directly accessible, but you will
find it hidden within your home directory. Prefix the commands with the path, so `jupyter` becomes
`~/.local/bin/jupyter`. If you feel like it, add this `bin` directory to your `PATH`.


## Making the PySpark kernel available in Jupyter

Review and edit the `kernel.json` file. At the very least, replace `/opt/spark` with the actual
path to your Spark installation. Make sure you use the same Python executable for the Spark
driver (under the `argv` property) and the executors (under the `PYSPARK_PYTHON` environment
variable). Finally, edit the `PYSPARK_SUBMIT_ARGS` variable to use the resources available.

If you are running Spark on a single machine without launching master and worker processes, you can
run Spark in local mode. For example, replace the first argument with `--master local[3]`, where
the number between brackets in the number of CPU cores to allocate to Spark. If you use a cluster
or run Spark in standalone mode, specify the amount of memory and CPU cores you are requesting.
Refer to the Spark documentation for all the possible interesting options.

On Linux systems, create a new directory under `~/.local/share/jupyter/kernels` with the name of
the kernel to create. For example:

    mkdir -p ~/.local/share/jupyter/kernels/pyspark

Copy the `kernel.json` file into that directory.

You may run `jupyter kernelspec list` to display the list of available kernels. The PySpark kernel
should be visible in that list. (Use `~/.local/bin/jupyter kernelspec list` if installed in user
mode).

    $ jupyter kernelspec list
    Available kernels:
      python3    /home/phil/.local/lib/python3.5/site-packages/ipykernel/resources
      ir         /home/phil/.local/share/jupyter/kernels/ir
      pyspark    /home/phil/.local/share/jupyter/kernels/pyspark


## Launching the notebook Web application

You're ready to launch Jupyter. Run `jupyter notebook` (or
`~/.local/bin/jupyter notebook`) and start the notebook. After a few seconds,
Spark should have launched (check for errors). Fix the paths to source data to
match your own environment and execute all the cells.


## Issues and improvements

The code and these instructions will probably not work for everyone, but it you manage to get an
error message, I can try to bring some improvements. Although this notebook is not meant to be
used in a general way, improvements such as clarifications and fixes are really welcome, so please
fork the repository and create a pull request.

Have fun!
