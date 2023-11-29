# PSRBENCH

___“Test how fast your hardware is for pulsar research!”___

PSRBENCH is a code that allows you to benchmark your hardware when using it for pulsar searching.


## Requirements

At minimum, PSRBENCH requires:
- [*crucial*] Python 3.8 or newer with the [Numpy](https://numpy.org/) library
- [*crucial*] [PRESTO 3.0](https://github.com/scottransom/presto) or newer

For the GPU benchmark:
- [*optional*] A CUDA-compatible GPU (i.e. an NVIDIA GPU) and Jintao Luo's [PRESTO2_ON_GPU](https://github.com/jintaoluo/presto2_on_gpu)    




## Installation

### Docker / Singularity
The easiest way to use PSRBENCH is by downloading one of its Docker image:

    docker pull alex88ridolfi/psrbench:ampere-sm86

and run the code from within the image:

    docker run -ti alex88ridolfi/psrbench:ampere-sm86

Clearly, you can use Singularity/Apptainer, if you prefer so:

    singularity pull docker://alex88ridolfi/psrbench:ampere-sm86

and run the code from within the image with:
    
    singularity shell --nv psrbench_ampere-sm86.sif
or

    singularity shell --nv --nvccli psrbench_ampere-sm86.sif

    

### Manual installation
Otherwise, you can install PSRBENCH and its dependencies manually.
    
PSRBENCH itself does *not* require any installation procedure. 

1) Once you made sure that you have Python 3.8+ and PRESTO 3.0+ installed, you can simply get the latest version of PULSAR_MINER by downloading the git repository: 

   `git clone https://github.com/alex88ridolfi/psrbench`


2) If you want to have PSRBENCH and its auxiliary tools always at hand, add the PULSAR_MINER directory to your `~/.bashrc` file:

   `echo "export PATH=/path/to/psrbench:\${PATH}" >> ~/.bashrc`

   where, of course, `/path/to/psrbench` must be replaced with the actual path of the downloaded repository.

3) Log-out and re-login to your terminal to make the changes effective.

#### GPU Acceleration

To enable the GPU part of the benchmark: 

4.  Install CUDA version 11.8 or older on your system

    **Note**: Remember that, even if your system already has CUDA 12.0 or newer installed, you can always install an older version of CUDA alongside your main one. See installation notes on [this forked version of PRESTO2_ON_GPU](https://github.com/alex88ridolfi/presto2_on_gpu)


5.  Install PRESTO2_ON_GPU with CUDA enabled.

    - If you are using CUDA version <= 11.5.2,  install Jintao Luo's  [original version of PRESTO2_ON_GPU](https://github.com/jintaoluo/presto2_on_gpu) 
    - If you are using CUDA version 11.6 to 11.8, install the [forked version of PRESTO2_ON_GPU](https://github.com/alex88ridolfi/presto2_on_gpu), which should also be a tiny bit easier to install.

6. Make sure to have the `PRESTO2_ON_GPU` environment variable with the path to your PRESTO2_ON_GPU installation
 
   `echo "export PRESTO2_ON_GPU=/path/to/presto2_on_gpu" >> ~/.bashrc `


## Basic usage
To run the CPU benchmark:

    psrbench -tests accelsearch_CPU

To run the GPU benchmark:

    psrbench -tests accelsearch_GPU

To run both the CPU and GPU benchmarks:

    psrbench -tests accelsearch_GPU,accelsearch_CPU

By default PSRBENCH runs PRESTO's `accelsearch` with the `zmax` values of 25,50,75,150,300,600 and 1200.
These values can be customized by using the `-zmax` option of PSRBENCH.
For example, if I wanted to run the tests with the `zmax` values of 200,400,600, I would run:

    psrbench -tests accelsearch_GPU,accelsearch_CPU -zmax "200,400,600"

By default, when accelsearch is run on CPU, it uses 10 CPU threads and sums 8 harmonics (`-ncpus 10 -numharm 8`).

By default, when accelsearch is run on GPU,	it uses the GPU number "0", 1 CPU thread, and sums 8 harmonics (`-cuda 0 -numharm 8`).

These behaviours can be changed with the `-flags_accelsearch_cpu` and `-flags_accelsearch_gpu` options, respectively.
For instance, if I want to use only 2 threads for accelsearch on CPU, use my second GPU on my system (GPU id "1") and sum only 4 harmonics in both, I would run:

    psrbench -tests accelsearch_GPU,accelsearch_CPU -flags_accelsearch_cpu "-ncpus 2 -numharm 4" -flags_accelsearch_gpu "-cuda 1 -numharm 4" -zmax "200,400,600"

At the end of the run, PSRBENCH produces an output plot saved as `psrbench_histogram_YYYYMMDD_HHMMSS.png`, where `YYYYMMDD_HHMMSS` is the date and time at which thecode was started.

You can also ask PSRBENCH to show you the plot at the end of the run using the `-D` option:

    psrbench -tests accelsearch_GPU,accelsearch_CPU -zmax "200,400,600" -D

        
## References
If you effectively used PSRBENCH for your work, I would appreciate if you could cite the [PSRBENCH GitHub repository](https://github.com/alex88ridolfi/psrbench).

Thanks!

Alessandro Ridolfi



