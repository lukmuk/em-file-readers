# Electron Microscopy Image Readers

This is a (non-exhaustive) list of freely available software for reading and handling different vendor file formats in electron microscopy.

Feel free to contribute PRs to update the list!

| Format            | Vendor          | Software                                                                                             | Plugin / Package                                                                                                                                                                                                                                                                     | Comments                                                                                                                                                                                                                     |
|:----------------- | --------------- | ---------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| tif<br/>(TFS/FEI) | TFS/FEI         | [ImageJ](https://imagej.nih.gov/ij/download.html)/[Fiji](https://fiji.sc/)                           | [Bio-Formats Importer](https://docs.openmicroscopy.org/bio-formats/5.8.2/users/imagej/installing.html), [EM tool](https://imagej.net/plugins/imbalence)                                                                                                                    | Start *Bio-Formats Importer* from the plugin menu.                                                                                                                                                                           |
|                   |                 | Python                                                                                               | [HyperSpy](http://hyperspy.org/hyperspy-doc/current/user_guide/io.html)/[RosettaSciIO](https://hyperspy.org/rosettasciio/supported_formats/tiff.html), [imageio](https://imageio.readthedocs.io/en/v2.9.0/format_fei.html), [tifffile](https://pypi.org/project/tifffile/) | tifffile examples: [1](https://stackoverflow.com/questions/54526139/extracting-scale-bar-from-tif-image-metadata-using-pil-tifftags),[2](https://stackoverflow.com/questions/72076758/adding-custom-extratags-with-tifffile) |
|                   |                 | [DigitalMicrograph/GMS](https://www.gatan.com/products/tem-analysis/gatan-microscopy-suite-software) | temDM’s “[ImportImage](https://temdm.com/open-source/)”                                                                                                                                                                                                                    | temDM: Push CTRL while starting the plugin will batch import all images in the folder.                                                                                                                                       |
| emi/ser           | TFS/FEI         | [ImageJ](https://imagej.nih.gov/ij/download.html)/[Fiji](https://fiji.sc/)                           | [TIA Reader](https://imagej.nih.gov/ij/plugins/tia-reader.html), [EM tool](https://imagej.net/plugins/imbalence), [CSI](http://spectrumimager.com/)                                                                                                                                                           | EM tool: Use "TEM .ser .dm3 folder export" to batch convert to scaled TIFF. <br/> TIA Reader: Will open multidimensional datasets, e.g. image series/spectrum images (spectra = single 1D "images"). <br/>CSI: Use for spectrum images.                                                                                                                                             |
|                   |                 | Python                                                                                               | [HyperSpy](http://hyperspy.org/hyperspy-doc/current/user_guide/io.html)                                                                                                                                                                                                    |                                                                                                                                                                                                                              |
|                   |                 | [DigitalMicrograph/GMS](https://www.gatan.com/products/tem-analysis/gatan-microscopy-suite-software) | temDM’s “[ImportImage](https://temdm.com/open-source/)”                                                                                                                                                                                                                    | temDM: Push CTRL while starting the plugin will batch import all images in the folder.                                                                                                                                       |
| dm3               | Gatan           | [ImageJ](https://imagej.nih.gov/ij/download.html)/[Fiji](https://fiji.sc/)                           | Built-in reader, [EM tool](https://imagej.net/plugins/imbalence), [CSI](http://spectrumimager.com/)                                                                                                                                                                                                           | Built-in reader: No metadata other than image scale (confirm?).<br/>EM tool: Use "TEM .ser .dm3 folder export" to batch convert to scaled TIFF.<br/>CSI: Use for spectrum images.                                                                              |
|                   |                 | Python                                                                                               | [HyperSpy](http://hyperspy.org/hyperspy-doc/current/user_guide/io.html)                                                                                                                                                                                                    |                                                                                                                                                                                                                              |
|                   |                 | [DigitalMicrograph/GMS](https://www.gatan.com/products/tem-analysis/gatan-microscopy-suite-software) | Built-in reader                                                                                                                                                                                                                                                            |                                                                                                                                                                                                                              |
| dm4               | Gatan           | [ImageJ](https://imagej.nih.gov/ij/download.html)/[Fiji](https://fiji.sc/)                           | [Bio-Formats Importer](https://docs.openmicroscopy.org/bio-formats/5.8.2/users/imagej/installing.html)                                                                                                                                                                     | Start *Bio-Formats Importer* from the plugin menu.                                                                                                                                                                           |
|                   |                 | Python                                                                                               | [HyperSpy](http://hyperspy.org/hyperspy-doc/current/user_guide/io.html)                                                                                                                                                                                                    |                                                                                                                                                                                                                              |
|                   |                 | [DigitalMicrograph/GMS](https://www.gatan.com/products/tem-analysis/gatan-microscopy-suite-software) | Built-in reader                                                                                                                                                                                                                                                            |                                                                       |
| emsa, msa               | [MSA](https://www.microscopy.org/resources/scientific_data/) | [NIST-DTSA II](https://cstl.nist.gov/div837/837.02/epq/dtsa2/index.html)                                                                                                | Built-in reader                                                                                                                                                                                                    |
|                |  | Python                                                                                               | [HyperSpy](http://hyperspy.org/hyperspy-doc/current/user_guide/io.html)                                                                                                                                                                                                    |
|                |  | [DigitalMicrograph/GMS](https://www.gatan.com/products/tem-analysis/gatan-microscopy-suite-software)                                                                                               | Built-in reader                                                                                                                                                                                                     |  Rename .emsa files to .msa.
| bcf               | Bruker (Esprit) | Python                                                                                               | [HyperSpy](http://hyperspy.org/hyperspy-doc/current/user_guide/io.html)                                                                                                                                                                                                    | Only EDS data, no EBSD.                                                                                                                                                                                                      |
# Workflows and other tips

#### TIA .emi/.ser EELS/EDS Spectrum Image to DigitalMicrograph  
FEI/TFS microscopes without DigiScan acquire spectrum images (SIs) through the microscope interface (*Experiments* tab).  
DigitalMicrograph offers a nice GUI for processing the data, e.g., [NLLS fitting of ELNES](https://www.youtube.com/watch?v=bYnN0DaRMaI) features.  
To transfer the SI data:
  - Load .emi/.ser SI data into HyperSpy
  - Save as .rpl/.raw files
  - Use [ImportRPL](https://github.com/hyperspy/ImportRPL) plugin to load .rpl/.raw data into DM  

A notebook (STEM-SI-Converter) can be downloaded [here](https://publikationen.bibliothek.kit.edu/1000144208).
