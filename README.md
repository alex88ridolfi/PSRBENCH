# PSRBENCH

___“Test how fast your hardware is for pulsar research!”___

PSRBENCH is a code that allows you to benchmark your hardware when using it for pulsar searching.


## Requirements

At minimum, PSRBENCH requires:
- [*crucial*] Python 3.8 or newer with the [Numpy](https://numpy.org/) library
- [*crucial*] [PRESTO 3.0](https://github.com/scottransom/presto) or newer

For the GPU benchmark:
- [*optional*] A CUDA-compatible GPU (i.e. an NVIDIA GPU) and Jintao Luo's [PRESTO2_ON_GPU](https://github.com/jintaoluo/presto2_on_gpu)    

    
If present, PSRBENCH can also benefit from:    
- [*optional*] the PRESTO Python3 libraries




## Installation

### Docker
The easiest way to use PSRBENCH is by downloading one of its Docker images and run it from there.


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

## References
If you effectively used PULSAR_MINER for your work, I would appreciate if you could cite the [PSRBENCH GitHub repository](https://github.com/alex88ridolfi/psrbench).

Thanks!

Alessandro Ridolfi



