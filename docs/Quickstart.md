# Quick Start

## Install Pre-Requisites

- Python 3
- Docker
- `git`
- `head`
- `xxd`

For generating C, Rust, and Go gitoids:
- `ar`
- `readelf`
- `objcopy`

For generating Java gitoids:
- Java
- `zip`
- `diff`

## Compile Bombash and Bomtrace from Source

```bash
git clone https://github.com/git-bom/bomsh.git bomsh
cd bomsh
docker build -t bomsh .devcontainer
# Copies the bombash/bomtrace/bomtrace2 binaries to the current working directory
docker run -it --rm -v ${PWD}:/out bomsh
```

## Generate GitBOM Docs

For C, Rust, and Go:

```bash
cp scripts/bomsh_hook2.py /tmp
cp scripts/bomsh_create_bom.py /tmp
bomtrace2 <build command>
# Generates the GitBOM metadata in treedb.json
python3 bomsh_create_bom.py -r /tmp/bomsh_hook_raw_logfile -j treedb.json
```

For Java:

```bash
# Generates the GitBOM metadata in treedb.json
python3 bomsh_create_bom_java.py -r <root directory of build workspace> -f <list of comma-separated jar files> -j treedb.json
```

