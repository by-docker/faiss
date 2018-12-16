# faiss

## Build docker container
> make container

This container is built from v1.4.0 [faiss](https://github.com/facebookresearch/faiss), including
the GPU option. Python 3.5.2 is used.

## Run docker container

```bash
# run a simple test
docker run --rm faiss python /opt/faiss/tests/test_build_blocks.py
# run on GPU
docker run --runtime nvidia --rm \
-v /usr/local/cuda-8.0/targets/x86_64-linux/lib:/usr/local/cuda-8.0/targets/x86_64-linux/lib \
faiss python -c 'import faiss; print(faiss.get_num_gpus());'
```

## Build docker container with Jupyter
> make jupyter

## Run docker container with Jupyter
```bash
make run_notebooks NOTEBOOKS_DIR=$ABSOLUTE_PATH
```
