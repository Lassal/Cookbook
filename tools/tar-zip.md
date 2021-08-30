# Extract & compact tools

## Tar

### Extract tar gz

Extract current tar file in the current directory.

  - x : extract
  - v : verbose
  - f : tar file name

```bash

# Extract current tar file in the current directory.
#   -x : extract
#   -v : verbose
#   -f : tar file name
tar -xvf file.tar

# Extract tar file in the output-directory
#  - C : output directory
tar -C output-directory -xvf file.tar

```

