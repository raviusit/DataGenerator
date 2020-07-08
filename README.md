# Data Generator

## Description
A generic data generator that's fast and extendable.

This is a Python 3 project which is used to generate large amounts of complex data sets which mimics real world data

Demo Data Generator requires a JSON configuration file to read the schema configuration of the various tables you want to generate. Here we will describe the format of the configuration file and enumerate the different parameters you can use to generate the data you want.

The overall structure of the configuration file looks like the following:

{
    "Defaults": {
        ...
    }, 
    "Services": [
        ...
        ...
    ],
    "Tables": {
        ...
        ...
        ...
        ...
    }
}

## Requirements
* Python (>= 3.7)

## Installation

```
$ cd DataGenerator
$ pip3 install dist/*.whl
```
Test if successfully installed
```
$ dg --version
```
*optional*: install tqdm for progress bar
```
$ pip3 install tqdm
```

## Usage
Get a list of all command line options by running
```
$ dg --help
```
***Basic Usage***: write a config file (say config.json) and run the data generator as follows:
```
$ dg config.json
```
Learn how to write a configuration file for the data generator

#### Command Line Options
**-n, --samples**

Instead of generating the number of rows specified in the config file,
generate only the number of rows specified by this argument

*sample usage*
```
$ dg -n 5 config.json
```

**-C, --commit**

Use this argument to save any changes made to config the file

*sample usage*
```
$ dg -C config.json
```

**-d, --rundate**

If you use 'today' in any of the date generators in your config,
then supplying this argument will use the date provided instead of
today's date. The format of the date is mm/dd/yyyy by default.
But this can be changed in the config.

*sample usage*
```
$ dg -d 01/01/2015 config.json
```

**-s, --start**

Suppose the config file has configurations for 10 tables, or you specify 10 tables
in "order" under the "Tables" section of the config, then specifying this argument
will start generating data from the index specified. (indexing is 0 based).
```
$ dg --start 3 config.json
```

**--plug**

Use this argument to plug in any custom generators, services or posts that you need
for generating your data. Learn how to write custom generators, services and posts

Suppose your custom scripts are in a directory called "custom", then
```
$ dg --plug custom config.json
```
will plug in the scripts and can be used by the datagenerator for generation.

**-o, --only**

Use this argument if you want to generate data for only a specific set of tables in the
configuration. You can specify one or more tables.
Use this argument only after the the configuration file name.

*sample usage*
```
$ dg config.json -o Customer Address
```

**-e, --exclude**

If you want to exclude one or more tables from the generation process you can list them here.
Use this argument only after the the configuration file name.

*sample usage*
```
$ dg config.json -e Order OrderItem
```

