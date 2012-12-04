timepy (time flies py)
----------------------

An easy way to quickly evaluate the performance of competing commandline
scripts, arguments, applications, or even apps. It's all packed into
a simple python script that takes advantage of the standard python
`timeit` module. It should give a good general idea of the speed of a
program and allow you to compare multiple versions to make an informed
decision.

*Requirements*: Matplotlib, numpy

## Usage

The help for `timepy` can always be looked at with `timepy -h` from the
commandline, which yields:

    timepy
    usage: timepy [-h] [-n NUMBER] [-r REPEAT] [-b BINS] [-d DATA_FILE]
                [-f FIG_FILE] [-v] [--hist] [--load]
                stmt [stmt ...]

    positional arguments:
    stmt                  The system statement to run, comparison is done if
                            more than one are provided

    optional arguments:
    -h, --help            show this help message and exit
    -n NUMBER, --number NUMBER
                            How many times to execute the statement
    -r REPEAT, --repeat REPEAT
                            How many times to repeat the timer
    -b BINS, --bins BINS  Number of bins in the histogram
    -d DATA_FILE, --data-file DATA_FILE
                            Specify the output file for the data
    -f FIG_FILE, --fig-file FIG_FILE
                            Specify the output file for the figure
    -v, --verbose         Print the output of every command to stdout
    --hist                Plot the histogram instead of filled curve
    --load                Loads the data from a data-file and plots it

As you can see, there is access to data files and figures to help
visualize the performance. My motivation for this script was a slow
script I created for [tmux-powerline][tp], which caused visual glitches
in my terminal. To fix this, I created a couple possibilities and needed
a way to test them. As you can see in the figure, I can safely choose
the new method because it is just as fast as the "fast" version and it
retains needed compatibility.

![vcs-compare](/img/vcs-compare_time.png)

This was all produced by the simple command (of course, the `$`
signifies the commandline):

    $ timepy -r 100 -f plot2.png -d data.txt ./original_1.0 ./fast_incompatible ./new_compatable

## Interpretation

Because the `timeit` command can be occasionally thrown off by
background processes, the data in the figure should be interpretted
with good judgement. That being said, it does not represent a good
statistical distribution under most circumstances. The relevant part of
the [python docs][timeit] says it best:

> *Note* It’s tempting to calculate mean and standard deviation from the
> result vector and report these. However, this is not very useful. In a
> typical case, the lowest value gives a lower bound for how fast your
> machine can run the given code snippet; higher values in the result
> vector are typically not caused by variability in Python’s speed, but
> by other processes interfering with your timing accuracy. So the min()
> of the result is probably the only number you should be interested in.
> After that, you should look at the entire vector and apply common sense
> rather than statistics.

So, to sumarize, you are better off focusing on the lower-end of each
histogram produced and not try to measure mean or standard deviation.

## Feedback

`timepy` should be open and useful to anyone interested, please feel
free to use it. If you think it's missing functionality or needs fixing,
please fork it and let me know!

[tp]:https://github.com/erikw/tmux-powerline
[timeit]:http://docs.python.org/2/library/timeit.html
