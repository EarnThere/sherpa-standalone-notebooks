
# Notebooks for Sherpa

IPython notebooks showing off how to use either the
[standalone version](https://sherpa.readthedocs.io/en/latest/)
or [CIAO](http://cxc.harvard.edu/sherpa/)
version of Sherpa to fit data. They were originally intended for the
standalone version, but it's now easy to run Jupyter notebooks in CIAO
(as of the 4.11 release) so you can use both.

---

You can use the MyBinder service to run these notebooks in your
browser, without having to install *anything*, by clicking on the
"launch binder" button below. It can take a little time to start up!

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/DougBurke/sherpa-standalone-notebooks/master)

---

# What is the difference between CIAO and standalone Sherpa

The main differences between using the standalone version of
Sherpa and that provided in CIAO are:

- CIAO comes with support for the [XSPEC model library](https://heasarc.nasa.gov/xanadu/xspec/manual/node308.html) whereas you have to compile both
[XSPEC and Sherpa](https://sherpa.readthedocs.io/en/latest/install.html#xspec)
when using the standalone release;
- CIAO uses Crates as its I/O libraray whereas the standalone release uses
AstroPy;
- CIAO uses ChIPS for plotting, although it comes with Matplotlib and you can
can change it (as we do in the MyBinder release)
- the release schedules of the two are different, so you may see slightly-different functionality in the latest released versions.

# How to run these notebooks

## Using MyBinder

I have used the [MyBinder service](https://mybinder.org/) to create an
environment that contains CIAO 4.11 (well, the Sherpa parts, so you
get XSPEC and matplotlib) which can be used to *run these notebooks
straight from your browser*. Awesome!

Note that most of the binders have not been re-run with CIAO 4.11, and
so may fail due to using Python 2.7 idioms (or changes in behavior, but
I don't expect there to be any of the latter).

## CIAO (New with CIAO 4.11)

CIAO 4.11 comes with both `jupyter notebook` support and includes Matplotlib,
so you can just enter

    > jupyter notebook

in this directory after starting CIAO (i.e. sourceing the `ciao.*sh` file
to match your shell).  If you are going this route, then it is *strongly*
suggested that you change your `.sherpa.rc` file in your home directory so
that Sherpa uses Matplotlib rather than ChIPS for its plots (as Matplotlib
is integrated with Jupyter notebooks whereas ChIPS is not). That is, you
should see

    > grep plot_pkg ~/.sherpa.rc
    plot_pkg : pylab

## Standalone Sherpa

We provide conda packages for Sherpa (and it is also `pip` installable),
so you can install Sherpa into a conda environment, along with the jupyter
notebook (or lab) enviroment. For example:

    > conda create -n=sherpa-notebooks -c sherpa python=3.7 sherpa jupyter matplotlib astropy
    > conda activate sherpa-notebooks
    > jupyter notebook

---

# The notebooks

These do not have to be read in the presented order, but some build
on previous ones. They are not guaranteed to be kept up to date!

 - [A really simple "fit"](http://nbviewer.ipython.org/github/DougBurke/sherpa-standalone-notebooks/blob/master/really%20simple%20fit.ipynb),
   which also doubles as my go-to-guide when cooking my kids porridge
   for breakfast.

   Last updated: March 28 2019 to use the Sherpa 4.11.0 release
 
 - [A simple fit](http://nbviewer.ipython.org/github/DougBurke/sherpa-standalone-notebooks/blob/master/simple%20sherpa%20fit.ipynb) which is based on
   the [NumPy/SciPy fitting example](http://python4astronomers.github.io/core/numpy_scipy.html)
   from the 
   [Practical Python for Astronomers](http://python4astronomers.github.io/index.html)
   course.

   Last updated: March 28 2019 to use the Sherpa 4.11.0 release
   
 - [Writing your own user model](http://nbviewer.ipython.org/github/DougBurke/sherpa-standalone-notebooks/blob/master/user%20model.ipynb),
   which fits the cumulative distribution function of a data set
   with the Gamma CDF. The same code can be run from the CIAO version
   of Sherpa (I added this as we are currently lacking in documentation
   for how to use the `add_user_model` routine).

   Last updated: March 28 2019 to use the Sherpa 4.11.0 release

 - [An integrated user model](http://nbviewer.ipython.org/github/DougBurke/sherpa-standalone-notebooks/blob/master/an%20integrated%20user%20model.ipynb),
   which fits the Gamma probability distribution function to the data
   set used in the 'Writing your own user model' example. This is
   an example of handling "integrated" data sets, and also shows off
   how to write a `guess` routine for your model, and some plot
   manipulations (in particular, re-creating a region-projection plot
   and adding extra annotations to it).

   Last updated: March 28 2019 to use the Sherpa 4.11.0 release

 - [How can I plot data and models when using the lower-level routines](http://nbviewer.ipython.org/github/DougBurke/sherpa-standalone-notebooks/blob/master/plotting%20using%20the%20lower-level%20routines.ipynb),
   which came up (in my mind) in the "Writing your own user model"
   example, where I started off using the lower-level API, but quickly
   switched to the higher-level (data management) API in part because
   I did not know how to create the plots. Well, I do know, and so
   can *you*.

   Last updated: March 28 2019 to use the Sherpa 4.11.0 release

 - [Extending existing models (and an example of using XSPEC models)](http://nbviewer.ipython.org/github/DougBurke/sherpa-standalone-notebooks/blob/master/extending%20existing%20models%20%28and%20XSPEC%29.ipynb),
   which shows how to write a user model that extends the behavior of
   an existing model (in this case, subtracting a model from itself with
   different parameter values). It also shows how to build the XSPEC module,
   and so use the
   [XSPEC models](https://heasarc.gsfc.nasa.gov/xanadu/xspec/manual/Models.html)
   from standalone Sherpa.

   Last updated: March 29 2019 to use with CIAO 4.11

   **NOTE** there appears to be a [bug with user models](https://github.com/sherpa/sherpa/issues/609) in CIAO 4.11 / Sherpa 4.11.0


 - [Simulating 2D data with a dash of error analysis](http://nbviewer.ipython.org/github/DougBurke/sherpa-standalone-notebooks/blob/master/simulating%20a%202D%20image%20and%20a%20bit%20of%20error%20analysis.ipynb),
   which uses the object API to simulate a 2D model (i.e. an image),
   fit it, and calculate errors on the parameters. This can be thought of
   as an extension of the previous notebooks that show how to replicate
   the functionality of the high-level UI layer using the object API
   (it also marks the start of me using the term "object API" for what I
   previously referred to as the "low-level API").

   Last updated: March 28 2019 to use the Sherpa 4.11.0 release

 - [Simulating and fitting a 2D image (this time with a Bayesian approach)](http://nbviewer.ipython.org/github/DougBurke/sherpa-standalone-notebooks/blob/master/simulating%20and%20fitting%20a%202D%20image%20%28this%20time%20with%20a%20Bayesian%20approach%29.ipynb),
   which is based on the previous notebook, this time showing how
   you can use the Monte Carlo Markov Chain (MCMC) analysis module
   in Sherpa (that is, the
   [Bayesian Low-Count X-ray Spectral (pyBLoCXS)](http://hea-www.harvard.edu/astrostat/pyblocxs/)
   module). This notebook is mainly intended to show *how* to do this,
   rather than explain why (or the differences between the various
   frequentist and Bayesian methods for coming up with an error estimate).

   Last updated: March 29 2019 to use the Sherpa 4.11.0 release

 - [An introduction to the Session object](http://nbviewer.ipython.org/github/DougBurke/sherpa-standalone-notebooks/blob/master/an%20introduction%20to%20the%20Session%20object.ipynb),
   which is a *very* brief example of how to use the Session object
   to access the UI API (e.g. that from sherpa.astro.ui or sherpa.ui)
   but with a more-Pythonic approach.

   Last updated: March 28 2019 to use the Sherpa 4.11.0 release
 
 - [Fitting a PHA dataset using the object API](http://nbviewer.ipython.org/github/DougBurke/sherpa-standalone-notebooks/blob/master/Fitting%20a%20PHA%20dataset%20using%20the%20object%20API.ipynb),
   which provides a quick runthrough showing how to use the object
   API to fit a PHA data set (that is, how in include the instrument
   response in a fit).

   Last updated: March 28 2019 to use the Sherpa 4.11.0 release

 - [Grouping spectra](https://nbviewer.jupyter.org/github/DougBurke/sherpa-standalone-notebooks/blob/master/grouping-spectra.ipynb), which looks
   at grouping PHA data to match plots produced by Sherpa. This isn't
   quite finished, but may be helpful to the [REXIS team](https://hea-www.harvard.edu/REXIS/class.html).

   This notebook uses [CIAO 4.11](http://cxc.harvard.edu/ciao4.11/).
   
   Last updated: March 14 2019 to add a section on errors and
   how to calculate them and match the plot results

# About these notebooks

The information in these notebooks is placed in the Public Domain and
is not an official product of the Chandra X-ray Center.
