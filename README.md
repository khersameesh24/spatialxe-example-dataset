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
pip install -r requirements.txt
```

Usage
```bash
$ python3 subset_data.py <path-to-xenium-bundle> <path-to-output-files>
```

Contact <br>
[Sameesh Kher](https://github.com/khersameesh24) - sameesh.kher@dkfz-heidelberg.de / khersameesh24@gmail.com <br>
[Florian Heyl](https://github.com/heylf) - florian.heyl@dkfz-heidelberg.de / flo.minion.info@gmail.com
