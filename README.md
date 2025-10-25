# ctranslate2-aarch64-cuda13-binaries
# CTranslate2 Binaries for DGX Spark (aarch64 / CUDA 13)

This release provides pre-compiled binaries for **CTranslate2 v4.6.0** built with CUDA support, specifically targeting NVIDIA DGX Spark systems.

## Build Environment

* **Hardware:** NVIDIA DGX Spark (Blackwell GB10 GPU, aarch64 architecture)
* **Operating System:** Ubuntu 24.04.3 LTS
* **Python:** 3.10.14 (via `pyenv`)
* **CUDA Toolkit:** 13.0 (Installed via `apt` from NVIDIA repo)
* **cuDNN:** 9.14.0 (Installed via `apt` from NVIDIA repo)
* **Compiler:** GCC 13.3.0
* **Build Flags:** `-DWITH_CUDA=ON -DWITH_CUDNN=ON -DWITH_MKL=OFF -DWITH_OPENBLAS=ON -DOPENMP_RUNTIME=NONE`

## Files

* `ctranslate2-cuda13-aarch64-dgxspark.tar.gz`: Archive containing the compiled C++ library and headers, installed under the `ctranslate2/` directory structure (intended for `/opt/ctranslate2`).

## Usage

1.  **Download:** Download the `.tar.gz` archive from this release.
2.  **Extract:** Extract the archive to your desired installation location, commonly `/opt`.
    ```bash
    sudo tar -xzvf ctranslate2-cuda13-aarch64-dgxspark.tar.gz -C /opt
    ```
3.  **Configure Linker:** Ensure the system's dynamic linker can find the library.
    ```bash
    echo "/opt/ctranslate2/lib" | sudo tee /etc/ld.so.conf.d/ctranslate2.conf
    sudo ldconfig
    ```
4.  **Install Python Wrapper (If Needed):** You still need to install the Python wrapper separately using `pip`. If building from source, ensure you point it to this installation:
    ```bash
    # Example for building from source:
    # cd /path/to/CTranslate2/source/python
    # CTRANSLATE2_ROOT=/opt/ctranslate2 pip install .
    ```
    Alternatively, install the standard pip package (which should now find the system library if `ldconfig` worked):
    ```bash
    # Ensure Python 3.10 env is active
    pip install ctranslate2
    ```

## Disclaimer

These binaries are provided as-is. Compatibility is only expected on systems closely matching the build environment. Always prefer building from source if possible.
