# salience-model
A model of visual salience written and developed by Rachel F Heaton and John E Hummel

* Copyright 2023 The Board of Trustees of the University of Illinois. All Rights Reserved.
* Licensed under the terms of the Apache License 2.0 license (the "License")
* The License is included in the distribution as License.txt file.
* You may not use this file except in compliance with the License.
* Software distributed under the License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
* See the License for the specific language governing permissions and limitations under the License.

# * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 
# Model of V1-based salience
## Developed and written by Rachel F Heaton and John E Hummel
#### This model profited from helpful conversations with Alejandro Lleras and Simona Buetti
# * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
This model was benchmarked on the MIT/Tuebingen Saliency benchmarks as
CASPER V1 Salience

https://saliency.tuebingen.ai/results.html

If this code is used for academic research, please cite the DOI to this repository:
<a href="https://doi.org/10.5281/zenodo.8429109"><img src="https://zenodo.org/badge/DOI/10.5281/zenodo.8429109.svg" alt="DOI"></a>

This code can be found at https://github.com/rachelfheaton/salience-model

# Acknowledgements
## This material is based upon work partly supported by the National Science Foundation under Grant No. BCS1921735

## This research is part of the Blue Waters sustained-petascale computing project, which is supported by the National Science Foundation (awards OCI-0725070 and ACI-1238993) the State of Illinois, and as of December, 2019, the National Geospatial-Intelligence Agency. Blue Waters is a joint effort of the University of Illinois at Urbana-Champaign and its National Center for Supercomputing Applications.

## A previous version of this material was based on research sponsored by the Air Force Research Laboratory, under agreement number FA9550-12-1-0003. The U.S. Government is authorized to reproduce and distribute reprints for Governmental purposes notwithstanding any copyright notation thereon.



# This code dynamically links Pillow which requires the following information to be included in any redistributions or uses:

The Python Imaging Library (PIL) is
   Copyright © 1997-2011 by Secret Labs AB
   Copyright © 1995-2011 by Fredrik Lundh
Pillow is the friendly PIL fork. It is
   Copyright © 2010-2023 by Jeffrey A. Clark (Alex) and contributors.
Like PIL, Pillow is licensed under the open source HPND License:
By obtaining, using, and/or copying this software and/or its associated
documentation, you agree that you have read, understood, and will comply
with the following terms and conditions:
Permission to use, copy, modify and distribute this software and its
documentation for any purpose and without fee is hereby granted,
provided that the above copyright notice appears in all copies, and that
both that copyright notice and this permission notice appear in supporting
documentation, and that the name of Secret Labs AB or the author not be
used in advertising or publicity pertaining to distribution of the software
without specific, written prior permission.

SECRET LABS AB AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS
SOFTWARE, INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS.
IN NO EVENT SHALL SECRET LABS AB OR THE AUTHOR BE LIABLE FOR ANY SPECIAL,
INDIRECT OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM
LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE
OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR
PERFORMANCE OF THIS SOFTWARE.

# This code dynamically links numpy which requires the following information to be included in any redistributions or uses:

Copyright (c) 2005-2023, NumPy Developers.
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:
   * Redistributions of source code must retain the above copyright
      notice, this list of conditions and the following disclaimer.
   * Redistributions in binary form must reproduce the above
      copyright notice, this list of conditions and the following
      disclaimer in the documentation and/or other materials provided
      with the distribution.
   * Neither the name of the NumPy Developers nor the names of any
      contributors may be used to endorse or promote products derived
      from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

# This code dynamically links MPI which requires the following information to be included in any redistributions or uses:

=======================
LICENSE: MPI for Python
=======================

:Author:       Lisandro Dalcin
:Contact:      dalcinl@gmail.com
:Web Site:     http://mpi4py.googlecode.com/
:Organization: CIMEC <http://www.cimec.org.ar>
:Address:      CCT CONICET, 3000 Santa Fe, Argentina


Copyright (c) 2013, Lisandro Dalcin.
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions
are met:

    * Redistributions of source code must retain the above copyright
      notice, this list of conditions and the following disclaimer.

    * Redistributions in binary form must reproduce the above
      copyright notice, this list of conditions and the following
      disclaimer in the documentation and/or other materials provided
      with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDER AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

# To run this code:
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
# 1. Install Python 3 
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

(This code was developed using Python 3.7)

Make sure the following modules/libraries are installed and available:
os, sys, math, datetime, numpy, Pillow, mpi4py

* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
# 2. Update the input and output path information for the images you want to run
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
These are found in the main() method at the bottom of runfilters_contrast.py
The default paths are

    inpath = './data/input_images/'
    
    outpath = './data/output_images/'

Put the files you want to analyze in the 'inpath' directory

* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
# 3. Open a terminal window and execute the following command in the directory where the code is located
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
mpirun -np 2 python3 -u -m mpi4py.futures ./runfilters_contrast.py 2
