---
layout: base
title: download
comments: true
---

# Download

If you have any trouble with the installation procedure below, please [contact me](/contact).

You will first need to install a version of R (see below), followed by several dependent R-packages, and finally the connectir R-package.

## R

### Redhat, CentOS, and Windows

Install the [community version of Revolution R](http://info.revolutionanalytics.com/download-revolution-r-community.html). This version of R is compiled with Intel's MKL, which provides parallel processing for matrix algebra operations even speeds up matrix algebra for one processor.

### Debian and Ubuntu

The community version of Revolution R should be available through your package manager.

### Other Versions of Linux

Install the [standard version of R](http://cran.r-project.org/mirrors.html).

### MacOSX

Install the [standard version of R](http://cran.r-project.org/mirrors.html). Maybe someone can confirm this: on older versions of OSX (pre Snow Leopard) you can open the application 'R' or 'R64' with the former being a 32-bit version of R. Make sure that you open the 64-bit version of R. In later versions, both applications are the 64-bit version of R.

## Package Dependencies

Open up the terminal and open R or Revo64 or R64, depending on your system. Now enter the following commands in the R prompt.

{% highlight r %}
install.packages(c("foreach", "doMC", "multicore", "getopt", "optparse"))
install.packages("plyr", dependencies=TRUE)
install.packages(c("Rcpp", "RcppArmadillo", "inline"), dependencies=TRUE)
install.packages(c("bigmemory", "biganalytics"), repos="http://R-Forge.R-project.org")
{% endhighlight %}

### Redhat, CentOS, Debian, Ubuntu, MacOSX, and Windows

Install bigalgebra as you did the other packages:

{% highlight r %}
install.packages("bigalgebra", repos="http://R-Forge.R-project.org")
{% endhighlight %}

### All Other Linux Systems

You will need to first install the Intel MKL library. A [free non-commercial version](http://software.intel.com/en-us/articles/non-commercial-software-download) is available for linux systems.

After you get the library, we will assume that it is installed in `/opt/intel/composerxe`. You can substitute this path as required. You will need to have the MKL library in your system library path. Run the following line in your terminal window and also add it to your .profile, .bashrc, or .bash_profile in your home directory ($HOME).

{% highlight bash %}
export LD_LIBRARY_PATH=/opt/intel/composerxe/mkl/lib/intel64:$LD_LIBRARY_PATH
{% endhighlight %}

Download the bigalgebra source code at https://r-forge.r-project.org/R/?group_id=556. Decompress the downloaded folder and in your terminal window navigate to this folder. Now enter the following 2 commands:

{% highlight bash %}
MKL_DIR=/opt/intel/composerxe/mkl

R CMD INSTALL --configure-args="
	--with-incDir='-DMKL_ILP64 -I${MKL_DIR}/include' 
	--with-blasHeader='mkl.h'
	--with-blas='-L${MKL_DIR}/lib/intel64/
		-lmkl_gf_ilp64 -lmkl_core -lmkl_def
		-lmkl_gnu_thread -lgomp'
	--with-lapack='-L${MKL_DIR}/lib/intel64/
		-lmkl_gf_ilp64 -lmkl_core -lmkl_def
		-lmkl_gnu_thread -lgomp'
	--with-lapackHeader='mkl.h'
	--with-int64='long long'" bigalgebra
{% endhighlight %}

## Connectir and Related Packages

You can install connectir and 2 related packages (niftir and big.extensions) by entering the following commands in the R prompt:

{% highlight r %}
install.packages(c("bigextensions", "niftir", "connectir"), repos="http://R-Forge.R-project.org")
{% endhighlight %}

Since I am actively developing this software, you may choose to install the svn version. Simply enter the following few commands in your terminal window:

{% highlight bash %}
svn checkout svn://scm.r-forge.r-project.org/svnroot/niftir
cd niftir/pkg
R CMD INSTALL bigextensions
R CMD INSTALL niftir
R CMD INSTALL connectir
{% endhighlight %}

## Scripts

To get the command-line scripts, navigate to: https://r-forge.r-project.org/scm/viewvc.php/pkg/connectir/inst/scripts/?root=niftir. If you downloaded and setup Revolution R, then download all the scripts with the **Revo** extension. Otherwise, download all the scripts with the **R** extension. You might want to rename each of those files so that they no longer have the **Revo** or **R** extension, since I assume there is no extension for these scripts in my documentation. You will also want to make these scripts. To do all this, enter the following commands in the directory with these scripts:

{% highlight bash %}
mv connectir_subdist.R connectir_subdist # replace .R with .Revo if you have RevolutionR
mv connectir_mdmr.R connectir_mdmr # replace .R with .Revo if you have RevolutionR
chmod u+x connectir_*
{% endhighlight %}

You might also want to put these directories somewhere on your path.
