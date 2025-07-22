# bSDD_dictionary_to_IDS

Convert a bSDD Dictionary into an IDS

## Description

This script is designed to convert bSDD dictionaries that define object types ("object dictionary"/"object type library" style) into a specific form of Information Delivery Specification (IDS). It is not intended for use with bSDD classes representing materials or groups of properties, and is not a comprehensive bSDD-to-IDS converter.

**Key points:**

- The script creates one IDS specification requiring any IFC object (from a default, non-comprehensive list of common entities, or a user-supplied list) to have a classification from the selected bSDD dictionary.
- For every class in the dictionary, it creates a requirement validating every object classified as that type from the dictionary.
- It does not (yet) support the full IFC schema, class inheritance, or validation of allowed property sets and data types.
- The script is tailored for practical use cases and may not cover all bSDD/IDS scenarios.

**Why use this?**
It helps automate the creation of IDS files for validating BIM models against object-type dictionaries published in bSDD, streamlining compliance checks and quality assurance workflows for typical object libraries.

**Limitations:**

- Not suitable for bSDD classes representing materials or property groups.
- Does not check IFC class inheritance or all allowed property sets.
- The included IFC entity list is not comprehensive; you can pass your own.

Contributions to improve coverage and functionality are welcome!

## Installation

Clone this repository to your local machine using:

```bash
git clone https://github.com/BIM-Tools/bSDD_dictionary_to_IDS.git
cd bSDD_dictionary_to_IDS
```

### Install Python dependencies

It is recommended to use a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the required packages using pip:

```bash
pip install -r requirements.txt
```

This will install all necessary dependencies, including `ifctester` and `tqdm`.

## Usage

To convert a bSDD dictionary into an IDS file, follow these steps:

1. **Find a Dictionary URI**:

   - Visit [buildingSMART Data Dictionary Search](https://search.bsdd.buildingsmart.org/).
   - Navigate through "List organizations" to find a specific dictionary version.
   - The Dictionary URI is typically in the format of `https://identifier.buildingsmart.org/uri/buildingsmart/ifc/4.3`, without any class at the end.

2. **Run the Script**:
   - Ensure Python is installed on your system.
   - Use the following command, replacing `<ids_file_path>` with your desired output file path, `<dictionary_uri>` with the URI you found, and optionally specifying the IDS version with `-v` or `--version`, another option is to add a comma separated list of applicable IFC entities:
     `python bsdd_to_ids.py <ids_file_path> <dictionary_uri> [-v VERSION]`

### Example Command

Here is an example command that demonstrates how to run the script:

```bash
python bsdd_to_ids.py basis_bouwproducten_oene.ids https://identifier.buildingsmart.org/uri/volkerwesselsbvgo/basis_bouwproducten_oene/latest -v 1.0 -i IfcWall,IfcSlab
```

## Help

```bash
usage: bsdd_to_ids.py [-h] [-v [{1.0,0.9.7}]] [-i IFC_ENTITIES] [-c] ids_file_path dictionary_uri

Generate IDS file from bSDD dictionary URI

positional arguments:
  ids_file_path         The filepath for the IDS file
  dictionary_uri        The URI for the dictionary

options:
  -h, --help            show this help message and exit
  -v [{1.0,0.9.7}], --version [{1.0,0.9.7}]
                        The IDS version (default: 1.0)
  -i IFC_ENTITIES, --ifc_entities IFC_ENTITIES
                        Applicable IFC entities
  -c, --use_cache       Use local cache

Example command: python bsdd_to_ids.py examples/basis_bouwproducten_oene.ids https://identifier.buildingsmart.org/uri/volkerwesselsbvgo/basis_bouwproducten_oene/latest
```

## Contributing

Contributions to improve the script or extend its functionality are welcome. Please refer to the contributing guidelines for more information.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
