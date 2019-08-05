# Cluster setup (specific to UNC)

Our lab primarily uses the killdevil cluster for computing. While you
may sometimes work locally on your laptop, you will eventually want to
also have the same code on the cluster, so you can run simulations for
example, without having to keep your laptop open and running. You may
also need to work on killdevil if you have data that cannot be
downloaded to a laptop.

The main pieces you need to work on killdevil are:

* X11 forwarding for when you SSH (so you can see plot windows)
* Some way of editing and running R code on the cluster,
  either [ESS](https://ess.r-project.org/)
  or [RStudio](https://www.rstudio.com/products/RStudio/) 
* Version control using [git](terminal_git_github.md).

## X11 forwarding

For Windows machines, you need to download and install an X11
application, such as Xming. (You may need to open Xming manually for
X11 forwarding to work when you connect to killdevil.)

<https://sourceforge.net/projects/xming/>

For Mac, you should install XQuartz. XQuart will open automatically
when you start an X11 forwarding session.

<https://www.xquartz.org/>

Then when you ssh to killdevil, you can use the following shell
command, where the -Y flag enables trusted X11 forwarding

```
ssh -Y username@killdevil.unc.edu
```

To test if this works, you can try the following in an interactive
shell and see if a plot open up.

```
module load r/3.4.1
R
> plot(1:10)
```

## Editing and running R code on the cluster

First, as always, you need to load an interactive shell with:

```
bsub -Is /bin/bash
```

I have these commands in my `.bashrc` file as aliases, so I don't have
to type this out each time:

```
alias inter='bsub -Is /bin/bash'
alias interbig='bsub -Is -M 10 /bin/bash'
alias interhuge='bsub -Is -M 20 /bin/bash'
```

For editing scripts and running R code this, I personally use emacs
and [ESS](https://ess.r-project.org/), but you can also load the
RStudio module on the cluster and work within an RStudio window. From
my experience there is too much lag in the window update, so it
restricts the speed of my typing / data analysis.

In order to use emacs you can put in your `.bashrc` file:

```
module load emacs
module load ess
module load r/3.4.1
```

Then in your `.emacs` file, add:

```
(require 'ess-site)
```

You can see
my [.emacs](https://gist.github.com/mikelove/b0f4eb15a21387ddb534)
file for more ESS customization. 

Assuming you know about emacs keybindings, to load R within emacs,
either type `M-x R` or you can start by running a line of code from an
R script with `C-c C-n`. See this reference card for ESS keybindings:

<http://ess.r-project.org/refcard.pdf>


## Version control using git

For editing data analysis R scripts or working on a new method, you
should be saving your code in git repositories, and typically also
syncing this with a BitBucket or GitHub remote server.
To use git on the cluster, you just need to have `module load git` in
your `.bashrc` file. You will have to set up SSH keys on the cluster,
to sync git repositories on the cluster with GitHub or BitBucket.
You can follow the steps described on the [the git page](terminal_git_github.md).

At the end, the ideal setup is to have GitHub repos on your laptop and
the same repo on the cluster, and you will use `git pull` to keep all
code up to date on all locations. You should `commit` and `push` your
code daily, to avoid any lost work.


