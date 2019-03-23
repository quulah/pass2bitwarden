# pass2bitwarden

A Python script to export data from [pass](https://www.passwordstore.org/) in [Bitwarden](https://bitwarden.com/) CSV format. This started as a quick and dirty script to move my passwords to Bitwarden, but it turned out worthy of being shared.

## Config

Currently, the parsed fields and any resulting formatting with regexp group matches or functions can be done in a `config.py` file.

By default the script exports data in the (Bitwarden Generic CSV Individual Account)[https://help.bitwarden.com/article/import-data/#generic-csv-format-individual-account] format.

The GPG encrypted password store data is decrypted and processed. As an example: `login_password` is grabbed from the first line of the data, `login_uri` is matched with `^url ?: ?(.*)$` and the `type` is always `login`. Check out the `defaults.py` file if you have any other requirements and create the `config.py` file.

Most likely, the `fields` and `notes` parsing could be implemented in some nice way by default. Feel free to create pull requests.

## Usage

```
$ ./pass2bw.py -h
usage: pass2bw.py [-h] [--directory DIRECTORY] [--gpg-binary BINARY]
                  [--output-file OUTPUT] [--gpg-agent]

Export password-store data to Bitwarden CSV format.

optional arguments:
  -h, --help            show this help message and exit
  --directory DIRECTORY, -d DIRECTORY
                        Directory of the password store.
  --gpg-binary BINARY, -b BINARY
                        Path to the GPG binary.
  --output-file OUTPUT, -o OUTPUT
                        File to write the CSV in.
  --gpg-agent, -a       Use GPG agent.
```

Example:

```
$ ./pass2bw.py -d ~/.password-store/subdir -a -o only_subdir.csv
```
