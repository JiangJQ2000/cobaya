# For release

## check PK_grid/interpolator changes for classy, and general classy review
# Global defaults for `oversample_power`, `burn_in`, etc
# Polychord: possible new release -- changes fast-slow behaviours, so waiting to do the oversample_power test.

# Incomplete implementations/bigger jobs
## Grids/rest of cosmomc scripts
## Lots of batchjob stuff (hasConvergeBetterThan,wantCheckpointContinue etc) now broken
## containers

# cosmetic/consistency/speed

## No output to files while burn in makes it hard to see if working OK (default no burn?) -- JT: should be ok now that it print sth every 60s?
## version attribute should be in all components not just theory (samplers can have versions) [done for samplers; missing: likelihoods]
## restrict external likelihood functions to those with no requirements/theory? (new class is almost as short, and avoids syntactic inconsistencies in _theory); or use _requirements, _provider?
## post: use MPI, and TODO's in code
## In the docs "Bases" (and UML diagram) not hyperlinked correctly (not sure how to fix)
## Make numba a requirement?
## dump log info along with each chain file if saving to file (currently in stdout)
## Faster Collections for MCMC: numpy cache for merging OnePoint into Collection, `_out_update` method would take care of flushing into the Pandas table.
## PolyChord: check overhead
## PolyChord: lower dimension tests?

# Enhancements/Refactorings

## some way to change default options, e.g. always use cobaya-run -f by default. Also argument to run() function.
## Support "parameterization" option of theory .yaml to specify parameter yaml variants?/generalize !defaults
## Let classes do all defaults combining; allow separate like instantiation + use equivalent to loading in cobaya
## `check_conflicts` theory method or similar (so likelihoods can raise error when used in combination with other variant likelihoods using non-independent data)
## If non-linear lensing on, model the non-linear correction via limber for faster semi-slow parameters
## minimize:
### unbounded parameters with flat prior (this would make it safe to rotate the unbounded ones in minimize) [JT: not very much in favour, since that would break a bunch of other stuff. Maybe let's explore an alternative solution?]
### add MINUIT
### maybe should not overwrite `sampler` block of original sample (either append or leave as it was)
## mcmc:
* finish removing .checkpoint in favour of updated.yaml and .progress
* For learning checks, X should perhaps ideally also depend slightly on the speed of the cycles, e.g. if either check becomes slow compared to a fast cycle.
* Update output thin factor once chains get over a given size, so that asymptotically the memory size of the chains doesn't grow indefinitely (and convergence checking time also doesn't grow correspondingly), just the thinning factor increases.
* more clever learning of covmat when only a few parameters missing: update only the row/columns of missing params, shrinkage estimator etc.
## CLASS: make it non-agnostic
## Regexp-ize checks for `COBAYA_INSTALL_SKIP` (in `install.py::_skip_helper`) and `COBAYA_TEST_SKIP` (in `conftests.py`), to be able to use underscores
## Test installed only (would need more clever pytest marking?)
## auto-covmats: separate parameter matching into slow ones and fast ones, and prefer missing some fast parameters than missing slow ones.
## auto-covmats: refactor to more be general and don't hard code Planck etc in main source (e.g. so external likelihood distributions can provide own covmat databases)
## doc, install, model may be better documented generally rather than only in cosmo sections.
## parameterization: there should be no need for "drop" if there are no agnostic components.