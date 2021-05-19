# Building Linux wheels with CUDA 11.0

The build scripts in this repo add the ```-Xcompiler -fno-gnu-unique``` flags
as suggested in https://github.com/pytorch/pytorch/issues/52663 .

Docker is required to build the linux wheels. The wheels can be build as
follows

```bash
# go to the builder root folder and start a docker container with the
# pytorch/manywheel-cuda110 image
sudo docker run -it --ipc=host --rm -v $(pwd):/remote pytorch/manylinux-cuda110 bash

# inside the container go to /remote/manywheel
cd /remote/manywheel

# define target python and pytorch version
export DESIRED_PYTHON=3.7
export PYTORCH_BUILD_VERSION=1.7.1
./build.sh
# after this the wheel is located in the wheelhouse110 directory in the
# repository root.
```

---
original README.md contents:

# pytorch builder

Scripts to build pytorch binaries and do end-to-end integration tests.

Folders:

- **conda** : files to build conda packages of pytorch, torchvision and other dependencies and repos
- **manywheel** : scripts to build linux wheels
- **wheel** : scripts to build OSX wheels
- **windows** : scripts to build Windows wheels
- **cron** : scripts to drive all of the above scripts across multiple configurations together
- **analytics** : scripts to pull wheel download count from our AWS s3 logs
- **test_community_repos** : scripts that test built binaries with various downstream repos that are high-priority and use pytorch
- **test_imports_docker** : some smoke tests to import torch in combination with other package imports, to check binary stability / compatibility
