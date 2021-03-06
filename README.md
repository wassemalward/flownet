<p align="center">
  <img height="150" src="https://raw.githubusercontent.com/equinor/flownet/master/docs/_static/flownet_logo.png">
</p>

<h2 align="center">Simplified training of reservoir simulation models</h2>

<p align="center">
<a href="https://badge.fury.io/py/flownet"><img src="https://badge.fury.io/py/flownet.svg"></a>
<a href="https://github.com/equinor/flownet/actions?query=workflow%3ACI"><img src="https://img.shields.io/github/workflow/status/equinor/flownet/CI"></a>
<a href="https://www.python.org/"><img src="https://img.shields.io/badge/python-3.6%20|%203.7-blue.svg"></a>
<a href="https://github.com/psf/black"><img src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>
<a href="https://lgtm.com/projects/g/equinor/flownet/alerts/"><img alt="Total alerts" src="https://img.shields.io/lgtm/alerts/g/equinor/flownet.svg?logo=lgtm&logoWidth=18"/></a>
<a href="https://lgtm.com/projects/g/equinor/flownet/context:python"><img src="https://img.shields.io/lgtm/grade/python/g/equinor/flownet.svg?logo=lgtm&logoWidth=18"></a>
</p>
<br/>

_FlowNet_ aims at solving the following problems:

* Create data-driven reduced physics models - directly from the data
* Train the model
* Assure model predictiveness
* Use the models to efficiently optimize and make decisions

For documentation, see [the GitHub pages](https://equinor.github.io/flownet/) for this repository.

## Contributing

Please check out our [contribution guidelines](CONTRIBUTING.md) if you want to contribute to FlowNet.

## Installation

_FlowNet_ is a Python package. The package itself, and other dependencies,
could be installed e.g. using a Python/Conda virtual environment. You will
need to choose your favourite environment and install all dependencies
to get going.

### Install FlowNet

_FlowNet_ uses the open-source reservoir simulator [_OPM-Flow_](https://opm-project.org/?page_id=19). To be able to run _FlowNet_ you will need to have _OPM-Flow_
installed first. There are also other dependencies like the Python packages [`libecl`](https://github.com/equinor/libecl) and
[`libres`](https://github.com/equinor/libres) which currently are not easily installable from PyPI (however, things are happening, so hopefully in a not too distant future, dependencies are installable from PyPI, which is already the case for flownet itself: `pip install flownet`).

##### 1. Clone the _FlowNet_ GitHub repository with SSH:
```bash
git clone git@github.com:equinor/flownet.git
```

##### 2. Move into the cloned directory:
```bash
cd flownet
```

##### 3. Run the scripts containing the building recipe: 
```bash
bash ./apt_insta.sh
bash ./build_environment.sh ./venv /usr/bin/flow
```
This will automatically create a simple [Python virtual environment](docs.python.org/3/library/venv.html) `./venv`

<details>
<summary><u>Click here</u> for alternative installation by creating your own environment</summary>

#### A. Python virtual environment
##### A.1. Create a [Python virtual environment](docs.python.org/3/library/venv.html) named `venv` yourself:
```bash
python3 -m venv ./venv
```
##### A.2. Activate the environment:
```bash
source ./venv/bin/activate
```
##### A.3. Run the build script providing the path to the Python virtual environment:
```bash
./build_environment.sh $VIRTUAL_ENV /usr/bin/flow
```
or
#### B. Conda environment
##### B.1. Create a [Conda environment](docs.conda.io/projects/conda/en/latest/user-guide/concepts/environments.html)
```bash
conda create -n venv python=3.7
```
##### B.2. Activate the environment:
```bash
conda activate venv
```
##### B.3. Fix path to Python packages:
```bash
conda create -n flownet python=3.7
conda activate flownet
echo "$CONDA_PREFIX/lib/python3.7/dist-packages" > $CONDA_PREFIX/lib/python3.7/site-packages/dist-packages.pth
```
##### B.4. Run the build script providing the path to the Conda environment:
```bash
./build_environment.sh $CONDA_PREFIX /usr/bin/flow
```

</details>

##### 4. Install the `flownet` Python module in development mode:
```bash
pip install -e .
```
Omit the `-e` flag if you want a standard installation.

> :warning: Do you want to run FlowNet through the LSF queue?
To be able to have the ERT process, that will be called by FlowNet,
run jobs via LSF correctly you will need to update your default shell's
configuration file (`.cshrc` or `.bashrc`) to automatically source your
virtual environment.
> 

### Install OPM-data (optional)

To be able to run examples that are dependent on the Norne field simulation,
you need to download the [OPM-data](https://github.com/OPM/opm-data) repository.
The preferred installation location is in the home directory, e.g. `~/opm-data`:

```bash
cd
git clone https://github.com/OPM/opm-data.git
```

### Running FlowNet

You can run _FlowNet_ as a single command line:
```
flownet ./some_config.yaml ./some_output_folder
```
Run `flownet --help` to see all possible command line argument options.

### Running webviz to check results

Before running `webviz` for the first time on your machine, you will need to to create a localhost `https` certificate by doing:
```bash
webviz certificate --auto-install --force
```

### Build documentation

You can build the documentation after installation by running
```bash
cd ./docs
make html
```
and then open the generated `./docs/_build/html/index.html` in a browser.

### License

FlowNet is, with a few exceptions listed below, [GPLv3](./LICENSE).

- The [Norne test data](./tests/data/norne.tar.gz) is available under the [Open Database License](http://opendatacommons.org/licenses/odbl/1.0/)
- The [FlowNet logo](./docs/_static/flownet_logo.png) is [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)
