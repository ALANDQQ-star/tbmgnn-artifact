# TBMGNN Artifact

This repository hosts the ACSAC artifact package for:

TBMGNN: Transferable Bot Detection Method Based on Multi-View Graph Neural Networks

The full artifact is distributed through the GitHub Release assets as split archive parts. Download all files named:

```text
tbmgnn_artifact.tar.gz.part-*
tbmgnn_artifact.tar.gz.sha256
```

Reassemble and verify on Linux or WSL:

```sh
cat tbmgnn_artifact.tar.gz.part-* > tbmgnn_artifact.tar.gz
sha256sum -c tbmgnn_artifact.tar.gz.sha256
tar -xzf tbmgnn_artifact.tar.gz
cd artifacts
chmod +x install.sh py.sh claims/*.sh claims/*/run.sh optional/*/run.sh
./install.sh
./claims/search/run.sh
./claims/ctu/run.sh
./claims/transfer/run.sh
./claims/ablation/run.sh
```

The checked artifact evaluation runs on Ubuntu 22.04 or 24.04, including WSL2, with Python 3, `python3-venv`, `pip`, and at least 16 GB RAM.
