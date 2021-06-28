# PyWarping
**Python module for face feature changing**

## Installation

```bash
pip install pywarping
```

If you get an error: `No such file or directory: 'cmake': 'cmake'`, you
need to make sure [cmake](www.cmake.org) is installed.  If you're on OSX you can install this via
Homebrew with:

```shell
brew install cmake
```

For other platforms please consult the Cmake documentation at <https://cmake.org/install/>

## Usage
For each face in an image define what **actions** are to be performed on it, `pywarping` will do the rest.
Check out the docs [here](https://github.com/dopevog/pywarping/tree/master/docs).
### Minimal Example
```python
import matplotlib.pyplot as plt

from pywarping.actions import Chubby, Multiple, Pipeline, Smile
from pywarping.detect import LandmarkFace

img_path = 'path/to/your/image'
img = plt.imread(img_path)

lf = LandmarkFace.estimate(img)

a_per_face = Pipeline([Chubby(), Smile()])
a_all = Multiple(a_per_face)

new_lf, _ = a_all.perform(lf)
new_lf.plot(show_landmarks=False, show_numbers=False)
```

### CLI
`pywarping` also comes with a CLI that exposes some
of its functionality. You can list the commands with `pw --help`:

```text
Usage: pw [OPTIONS] COMMAND [ARGS]...

  Automated face warping tool.

Options:
  --help  Show this message and exit.

Commands:
  list     List available actions.
  perform  Take an action.
```

To perform an action (Smile in the example below) and plot the result on the screen 
```bash
pw perform Smile INPUT_IMG_PATH
```

or if you want to create a new image and save it
```bash
pw perform Smile INPUT_IMG_PATH OUTPUT_IMG_PATH
```

## Notes
By default we are using a pretrained landmark model from https://github.com/davisking/dlib-models.

## License
This Project Has Been [MIT Licensed](LICENSE)