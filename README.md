# spatialxe-example-dataset
The repository shows the procedure followed to generate the example dataset for the nfcore-spatialxe pipeline 
[Xenium ranger](https://www.10xgenomics.com/support/software/xenium-ranger/latest) example dataset for the [nfcore-spatialxe](https://github.com/heylf/spatialxe) pipeline

Example dataset was downloaded from 10x Genomics website
Data : [Fresh Frozen Mouse Brain](https://www.10xgenomics.com/datasets/fresh-frozen-mouse-brain-for-xenium-explorer-demo-1-standard) - Tiny Subset

```bash
wget https://cf.10xgenomics.com/samples/xenium/1.0.2/Xenium_V1_FF_Mouse_Brain_Coronal_Subset_CTX_HP/Xenium_V1_FF_Mouse_Brain_Coronal_Subset_CTX_HP_outs.zip
```


Unzip the dataset, once unzipped the data size amounts to approx. 18Gb
```bash
unzip Xenium_V1_FF_Mouse_Brain_Coronal_Subset_CTX_HP_outs.zip
```

Install the following pip packages to run the python utility script
```bash
pip install spatialdata
pip install spatialdata_xenium_explorer 
```

Use the following python script to scale down the dataset
```python
#!/usr/bin/env python3

import sys
from pathlib import Path
from spatialdata import SpatialData
from spatialdata_io import xenium
from spatialdata_xenium_explorer import write


# generate the xenium spatialdata object
def generate_xenium_spatialobj(xenium_path: Path) -> SpatialData:
    """
    Generate a spatialdata obj from the xenium bundle
    Args:
    xenium_path - path to the xenium bundle from the XOA
    """
    sd_xenium_obj = xenium(xenium_path,
           n_jobs=1,
           cells_as_shapes=True,
           nucleus_boundaries=True,
           transcripts=True,
           morphology_mip=True,
           morphology_focus=True,
    )
    return sd_xenium_obj

# write xenium output files
def write_xenium_files(output_path: Path, sdata_obj: SpatialData) -> None:
    """
    Write xenium files on a path
    Args:
    output_path - path to write xenium files on
    sdata_obj - xenium spatialdata object
    """
    write(output_path, 
          sdata_obj, 
          image_key='morphology_focus', 
          shapes_key='cell_circles', 
          points_key=None, 
          gene_column='feature_name',
          pixel_size=0.2125, 
          spot=False, 
          layer=None, 
          polygon_max_vertices=13, 
          lazy=True,
          ram_threshold_gb=4, 
          mode=None
        )
    return None



if __name__ == "__main__":
    xenium_bundle = sys.argv[1]
    output_path = sys.argv[2]
    sd_xenium_obj = generate_xenium_spatialobj(xenium_path=xenium_bundle)
    write_xenium_files(output_path=output_path, sdata_obj=sd_xenium_obj)
```

Usage
```bash
python3 subset_data.py <path-to-xenium-bundle> <path-to-output-files>
```

Contact <br>
[Sameesh Kher](https://github.com/khersameesh24) - sameesh.kher@dkfz-heidelberg.de / khersameesh24@gmail.com <br>
[Florian Heyl](https://github.com/heylf) - florian.heyl@dkfz-heidelberg.de / flo.minion.info@gmail.com
