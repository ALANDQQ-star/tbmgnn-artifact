ACSAC artifact release for TBMGNN.

Download all split archive parts and the checksum file:

```text
tbmgnn_artifact.tar.gz.part-*
tbmgnn_artifact.tar.gz.sha256
```

Reassemble and verify:

```sh
cat tbmgnn_artifact.tar.gz.part-* > tbmgnn_artifact.tar.gz
sha256sum -c tbmgnn_artifact.tar.gz.sha256
```

Then unpack and run the checked evaluation:

```sh
tar -xzf tbmgnn_artifact.tar.gz
cd artifacts
chmod +x install.sh py.sh claims/*.sh claims/*/run.sh optional/*/run.sh
./install.sh
./claims/search/run.sh
./claims/ctu/run.sh
./claims/transfer/run.sh
./claims/table5/run.sh
./claims/ablation/run.sh
```

The checked workflows reproduce the CTU-13 result, transfer result, Table 5 comparison, reliability search, and ablation/statistical analyses described in the paper.
