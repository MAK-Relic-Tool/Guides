# Command Line Interface
Have an issue? Try the [Help](#help) section below.
## `relic`
Container for other commands

### Installation:
`pip install relic-tool-core`

### Usage
```
usage: relic [-h] {sga} ...

positional arguments:
  {sga}

optional arguments:
  -h, --help  show this help message and exit
```


## `relic sga`
Container for SGA commands, such as packing and unpacking.

Plugins for the version of SGA (E.G. V2 for Dawn of War I) need to be installed separately.

### Installation:
`pip install relic-tool-sga-core`

### Usage
```
usage: relic sga [-h] {pack,unpack} ...

positional arguments:
  {pack,unpack}

optional arguments:
  -h, --help     show this help message and exit
```

## `relic sga unpack`
Unpacks and decompresses an archive

Plugins for the version of SGA (E.G. V2 for Dawn of War I) need to be installed separately.

### Installation:
`pip install relic-tool-sga-core`

##### Optional Plugins
Dawn Of War: `pip install relic-tool-sga-v2`

### Usage
```
usage: relic sga unpack [-h] src_sga out_dir

positional arguments:
  src_sga     Source SGA File
  out_dir     Output Directory

optional arguments:
  -h, --help  show this help message and exit
```

## `relic sga pack`
Packs files into an SGA archive.

Plugins for the version of SGA (E.G. V2 for Dawn of War I) need to be installed separately.

### Installation:
`pip install relic-tool-sga-core`

##### Optional Plugins
Dawn Of War: `pip install relic-tool-sga-v2`

### Usage
```
usage: relic sga pack [-h] {v2} ...

positional arguments:
  {v2}

optional arguments:
  -h, --help  show this help message and exit
```

## `relic sga pack v2`
Packs files into an SGA archive.

Plugins for the version of SGA (E.G. V2 for Dawn of War I) need to be installed separately.

### Installation:
`pip install relic-tool-sga-v2`

### Usage
```
usage: relic sga pack v2 [-h] src_dir out_sga config_file

positional arguments:
  src_dir      Source Directory
  out_sga      Output SGA File
  config_file  Config .json file

optional arguments:
  -h, --help   show this help message and exit
```
### Config File
#### Sample
```json
{
  "test": {
	  "solvers": [
      {
        "match": "store.*",
        "storage": "store"
      },
      {
        "match": "*.buffer",
        "storage": "buffer"
      },
      {
        "match": "stream.txt",
        "storage": "stream"
      },
      {
        "match": "*.*",
        "storage": "store",        
        "query": "size > 0"
      }
    ]
  },
  "data": {
	  "path": "mymodata",
	  "solvers": [
		{
		   "match": "*.*",
		   "storage": "stream",     
       "query": "size >= 1000000000"
		},
		{
		   "match": "*.*",
		   "storage": "store",
		}
	  ]
  }
  "attrib": {
	  "path": "mymodattributes",
	  "solvers": [
		{
		   "match": "*.*",
		   "storage": "store",
		}
	  ]
  }
}
```
#### Config Explained
##### Solvers
`solvers` are how files are selected to be packed, they are executed *IN ORDER*. If a file has already been packed into the drive, it is ignored by following solvers.

##### Drive Name
`"test": {...}` and `"data": {...}`defines the drive that the files will be packed into. 
Typically this will be `"data"` or `"attrib"`.

##### Drive Path
`path` specifies the relative path from the `src_dir` specified when the command is called.
Files will be searched from the relative path instead of the `src_dir`.

##### Filtering with `match`
`match` is a standard glob filter.
`store.*` will grab any file that is named `store`, ignoring the extension.
`*.buffer` will grab any file with a `.buffer`  extension.
`stream.txt` will only grab files named `stream.txt`.
`*.*` will grab all files with a name and an extension.
`*` will grab all files, even those without extensions.

##### Filtering with `query`
Large files can be packed differently from small files via `query`
`query` supports any python expression, with `size` being the size of the file.
`size < 1000000000` will only include the file if it is less than 1 GigaByte.

##### Compressing Files
`"storage": ...` specifies how the file is packed. If omitted, `"store"` is used by default.
Options are:
* `"store"` :  File is not compressed.
* `"stream"` : File is zlib-compressed and marked for stream-decompression.
* `"buffer"` : File is zlib-compressed and marked for buffer-decompression.

# Help
### Invalid Choice Error
You may not have installed the command you are trying to run. Please try re-installing, using the `installation` section of the command on this page.

Your command may require an optional package to work properly, please refer to the `optional plugins` section of the command if applicable.

### I have a Bug or Problem
Please create an Issue on the [Issue Tracker](https://github.com/MAK-Relic-Tool/Issue-Tracker/issues). 
