OpenEXR
=======

**OpenEXR** is a high dynamic-range (HDR) image file format developed
by Industrial Light & Magic (ILM) for use in computer imaging
applications. It supports stereoscopic and deep images.  Weta Digital,
Walt Disney Animation Studios, Sony Pictures Imageworks, Pixar
Animation Studios, DreamWorks, and other studios, companies, and
individuals have made contributions to the code base. The file format
has seen wide adoption in a number of industries.

OpenEXR's features include:

* Higher dynamic range and color precision than existing 8- and 10-bit
  image file formats.
* Support for 16-bit floating-point, 32-bit floating-point, and
  32-bit integer pixels. The 16-bit floating-point format, called "half",
  is compatible with the half data type in NVIDIA's Cg graphics language
  and is supported natively on their GPUs.
* Multiple image compression algorithms, both lossless and lossy. Some of
  the included codecs can achieve 2:1 lossless compression ratios on images
  with film grain.  The lossy codecs have been tuned for visual quality and
  decoding performance.
* Extensibility. New compression codecs and image types can easily be added
  by extending the C++ classes included in the OpenEXR software distribution.
  New image attributes (strings, vectors, integers, etc.) can be added to
  OpenEXR image headers without affecting backward compatibility with
  existing OpenEXR applications. 
* Support for stereoscopic image workflows and a generalization
  to multi-views.
* Flexible support for deep data: pixels can store a variable-length list
  of samples and, thus, it is possible to store multiple values at different
  depths for each pixel. Hard surfaces and volumetric data representations
  are accommodated.
* Multipart: ability to encode separate, but related, images in one file.
  This allows for access to individual parts without the need to read other
  parts in the file.
* Versioning: OpenEXR source allows for user configurable C++
  namespaces to provide protection when using multiple versions of the
  library in the same process space.

License
-------

OpenEXR, including all contributions, is released under a modified BSD
license. Please see the ``LICENSE`` file accompanying the distribution
for the legal fine print.
      
OpenEXR Sub-modules
-------------------

The OpenEXR distribution consists of the following sub-modules:

* **IlmBase** - Utility libraries from Industrial Light & Magic: Half, Imath, Iex, IlmThread.
* **PyIlmBase** - Python bindings for the IlmBase libraries.
* **OpenEXR** - The core image library.
* **OpenEXR_Viewers** - Standard image viewing programs
* **Contrib** - Various plugins and utilities, contributed by the community.
    
Please see the ``README`` files of each of the individual directories for more information.

A collection of OpenEXR images is available from the adjacent repository
[openexr-images](https://github.com/openexr/openexr-images).

Dependencies
------------

OpenEXR depends on [zlib](https://zlib.net).

PyIlmBase depends on [boost-python](https://github.com/boostorg/python) and
optionally on [numpy](http://www.numpy.org).

In OpenEXR_Viewers:

* **exrdisplay** depends on [fltk](http://www.fltk.org/index.php)
* **playexr** depends on [Cg](https://developer.nvidia.com/cg-toolkit)

Web Resources
-------------

Main web page: http:://www.openexr.org

GitHub repository: http://www.github.com/openexr

Mail lists:

* **http://lists.nongnu.org/mailman/listinfo/openexr-announce** - OpenEXR-related announcements.

* **http://lists.nongnu.org/mailman/listinfo/openexr-user** - for discussion about OpenEXR applications or general questions.

* **http://lists.nongnu.org/mailman/listinfo/openexr-devel** - for developers using OpenEXR in their applications.

Building and Installation
-------------------------

Download the latest release of OpenEXR from
http://www.openexr.com/downloads.html.

To build the OpenEXR binaries from source, compile and install the
individual sub-models (IlmBase, PyIlmBase, OpenEXR, OpenEXR_Viewers),
according to the instructions in the respective ``README``
files. Build and install the IlmBase module first, then build and
install the OpenEXR module. Optionally, then build and install
PyIlmBase, OpenEXR_Viewers, and Contrib.

For the basic installation:

    cd <source root>/IlmBase
    ./configure
    make
    make install

    cd <source root>/OpenEXR
    ./configure
    make 
    make install

See the module ``README`` files for options to ``configure``.

#### Building from Git

Alternatively, you can download the latest release or the lastest
development branch directly from http://github.com/openexr.

After cloning the repo locally, generate the configuration scripts by
running the ``bootstrap`` script:

    cd <source root>/IlmBase
    ./bootstrap
    ./configure
    make
    make install

    cd <source root>/OpenExr
    ./bootstrap
    ./configure
    make
    make install

Building from git and ``bootstrap`` requires that **autoconf** is
installed.  Download and install it from
https://www.gnu.org/software/autoconf/autoconf.html.

#### Building with CMake

Alternatively, you can build with **cmake**, version 3.11 or newer. 

In the root ``CMakeLists.txt`` file, with -D options on the cmake
line, or by using a tools such as **ccmake** or **cmake-gui**,
configure the OpenEXR build. The options are detailed below.

Create a source root directory, cd into it, and run **cmake** to configure
the build.  Select an appropriate generator, such as "Unix Makefiles",
or "Visual Studio 15 2017 Win64". Then run **make** a the root
directory; this will build the appropriate submodules, according to
the settings of the **cmake** options, described below.

    cmake -DCMAKE_INSTALL_PREFIX=<install location> <OpenEXR source root> -G "selected generator" -DCMAKE_PREFIX_PATH=<paths to dependencies - zlib etc>
    make

The available options are:

* ``OPENEXR_BUILD_ILMBASE`` (ON)
By default, IlmBase is always built.

* ``OPENEXR_BUILD_OPENEXR`` (ON)
By default, OpenEXR is always built.

* ``OPENEXR_BUILD_PYTHON_LIBS`` (ON)
By default, the Python bindings will be built.

* ``OPENEXR_BUILD_VIEWERS`` (OFF)
By default, the viewers are not built, as they have not been updated for
modern OpenGL.

* ``OPENEXR_BUILD_SHARED`` (ON)
* ``OPENEXR_BUILD_STATIC`` (OFF)
The build can be configured to create either shared libraries, or static 
libraries, or both.

* ``OPENEXR_NAMESPACE_VERSIONING`` (ON)
OpenEXR symbols will be contained within a namespace

* ``OPENEXR_FORCE_CXX03`` (OFF)
C++03 compatibility is possible as an option

* ``OPENEXR_ENABLE_TESTS`` (ON)
By default, the tests will be built.

* ``OPENEXR_RUN_FUZZ_TESTS`` (OFF)
By default, the damaged input tests will NOT be run, due to their long
running time. If you wish to run them as part of "make test" (or equivalent
in your build system), then enable this. A "make fuzz" target will be
available to run the fuzz test regardless.

* ``OPENEXR_PYTHON_MAJOR``, ``OPENEXR_PYTHON_MINOR`` "2", "7"
By default, OpenEXR is built against Python 2.7.x.

## Documentation

Documentation is available at http://www.openexr.com/documentation.html.





Apache License
                           Version 2.0, January 2004
                        https://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS

   APPENDIX: How to apply the Apache License to your work.

      To apply the Apache License to your work, attach the following
      boilerplate notice, with the fields enclosed by brackets "[]"
      replaced with your own identifying information. (Don't include
      the brackets!)  The text should be enclosed in the appropriate
      comment syntax for the file format. We also recommend that a
      file or class name and description of purpose be included on the
      same "printed page" as the copyright notice for easier
      identification within third-party archives.

   Copyright 2019 Rolando Gopez Lacuata.

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       https://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
