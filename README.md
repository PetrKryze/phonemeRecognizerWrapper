# phonemeRecognizerWrapper
Package containing one wrapper script over the Allosaurus phoneme recognition library, designed for passing the Allosaurus output data to MATLAB scripts for further analysis.

## Installation
1. [Install Python 3](https://www.python.org/downloads/)
   - To see if Python is installed, use `py --version` in command line
   - `pip` is automatically included in the Python installation, but to check or update the pip version use: `py -m ensurepip --upgrade`
2. [Install this package](https://pypi.org/project/phonemeRecognizerWrapper)
   - From command line (assuming user has already installed python and pip):  
     `pip install phonemeRecognizerWrapper`
     - This should also automatically install all dependent packages. 

## Usage
This script uses the [Allosaurus](https://github.com/xinjli/allosaurus) phoneme recognition package to extract phonemic content from audio files of human speech. This script acts as a wrapper over the allosaurus package for improved formatting and piping of data to MATLAB scripts for analysis (e.g. vowel formant extraction).

### Command structure
`py -m phonemeRecognizerWrapper.recognize LANGUAGE_CODE FILES EMIT_PROB`

### Required Arguments:
1. `LANGUAGE_CODE`
   - Three characters long language code supported by the Allosaurus library. For the list of available languages, use command:  
     `py -m allosaurus.bin.list_lang`  
   - To display the phonetic inventory (list of phonemes) for a specific language, use:  
     `py -m allosaurus.bin.list_phone [--lang <language name>]`  
   - See [here](https://github.com/xinjli/allosaurus) for more info.
   - **Example options:**
     - `"ipa"` - uses the whole available phonetic inventory for recognition (less accurate)
     - `"deu"` - german
     - `"gsw"` - swiss german
     - `"fra"` - french
     - `"eng"` - english
2. `FILES`
   - Absolute path to a temp .txt file containing semicolon delimited text string of absolute paths to all files meant for recognition. Surround the string with apostrophes ("") if any of the paths contains spaces.
   - Temp file contents example:  
     `"C:\sounds\sound1.wav;C:\sounds\sound2.wav"`

### Optional Arguments:
3. `EMIT_PROB`
   - Allosaurus setting that determines the phoneme emission rate of the underlying model. Higher number tells the model to produce more phonemes, smaller number vice versa.  
   Center is at `1.0`, and optimal range that produces comprehensive outputs is `0.8 - 1.5`. **If omitted, default value of 1.5 is used.**

### Examples
- Example usage from command line:
  `py -m phonemeRecognizerWrapper.recognize eng "C:\sounds\sound.wav;C:\sounds\sound2.wav" 1.0`

- Example usage from MATLAB via the `[status, result] = system(command)` function:  
  `command = 'py -m phonemeRecognizerWrapper.recognize eng "C:\sounds\sound.wav;C:\sounds\sound2.wav" 1.0';`
  - It is also recommended to use `set PYTHONIOENCODING=utf8` before the python command to ensure proper text formantting via the standard output pipe.

## Contacts
> For any questions, please email: *petr.kryze@gmail.com*  
> Authors: Petr Krýže @PetrKryze based on code from Vojtěch Illner  
> CTU Prague, FEE 2023
