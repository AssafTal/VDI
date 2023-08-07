# VDI
Visual Display Interface (MRS Processing Library)

## What is VDI?
The Visual Display Interface (VDI) library is a set of open-source routines written in MATLAB for loading, preprocessing, visualizing, fitting and generally working with magnetic resonance spectroscopy (MRS) data, particularly in-vivo. It was written to provide practitioners a modern, object-oriented framework which they could use from the command line within MATLAB. The main guiding principle of VDI is reproducibility, which it attempts to promote by focusing on modern, well-documented code; and extensive reporting and logging capabilities.

## What can VDI Do?
The VDI libraries were initially conceived to deal with multiresolution
data, specifically high resolution anatomical images (such as T1-weighted
MPRAGE) and low resolution spectroscopic imaging (MRSI) data. The idea was to
create a library capable of applying manipulations to these joint datasets,
including:
* Calculating fractions of WM and GM in spectroscopic voxels
* Linear regression for global WM and GM MRSI concentrations
* Displaying MRSI maps correctly over high resolution MPRAGE images
* Masking MRSI data using high resolution anatomical images
* Shimming (high-res) B0 maps within spectroscopic voxels or slices.
* Getting averages of concentrations from high resolution masks defined 
  using (high resolution) atlases.
and so forth. 

Over time, additional functionality has been added:
* B0 shimming and shim coil mapping (via the VDIShims class).
* Interfacing MATLAB with LCModel for sending and receiving MRS data for
  fitting.
* Functions for efficiently processing MRS and MRSI data, including alignment,
  phasing, apodization, DC correction and so forth.


## Who is Responsible for VDI?
VDI originated in the laboratory of Assaf Tal, Ph.D., and features multiple contributers, mostly PhD and MSc students who have trained at the lab, who have contributed bits of code to its workings. Currently it is maintained by Assaf Tal.

## Overview and Structure
The VDI libraries are mostly built using object oriented programming. 
Functions are built into classes which often inherit from each other.
The main inheritance tree is the following:

                       VDIVolume-----------------+
                           |                     | 
                           |                     |
                          \|/                   \|/
                    VDIVolumeMatrix           VDIShape
                           |
                           |
                          \|/
                       VDIImage
                           |
                           |
                          \|/
                      VDIImageND

The base class VDIVolume provides the ability to define and work with
3D volumes and to orient them in space relative to some frame of reference
(the center of which coincides with the magnet's isocenter, i.e. the 
point where gradient-induced fields are zero). This is then built upon
to allow greater and greater structure:
* VDIShape is a class that is used to define shapes, either ellipsoids
  or boxes. It is used, e.g., to store VOI positioning, shimming volumes
  and so forth.
* VDIVolumeMatrix adds the additional ability to subdivide VDIVolume into
  voxels. It however does not have the ability to store or manipulate 
  3D data.
* VDIImage adds the ability to store & manipulate 3D data, and is the basic
  object used to handle images, such as MPRAGE or a B0 map.
* VDIImageND adds the ability to store and manipulate nD data and is the
  "go-to" class for storing and handling MRS and MRSI data (single voxel
  MRS data is just a 1x1x1xN dataset). 

## Examples
The classes themselves are thoroughly documented. More importantly, perhaps,
is the "examples" subdirectory, where you will find multiple documented
examples highlighting different uses for the libraries. 

## How to Cite?
If you wish to use the VDI libraries in your publication, please acknowledge
them in your citations. At the moment, there is no formal publication
describing them, so please cite them as computer software, and provide a
suitable link. For example:

Tal, A (2020). Visual Display Interface (VDI) [Computer Software]. Retrieved from http://www.vdisoftware.net
