NPU: Arrow Lake Intel
- Drivers: intel-fw-npu, intel-level-zero-npu, intel-driver-compiler-npu 1.35.0
- Loader: libze1 1.32.0 / 1.17.44 held
- ICD: /etc/level_zero/icd.d/intel_npu.icd
- Symlinks: libze_intel_vpu.so.1 -> libze_intel_npu.so.1.35.0
- OpenVINO: ['CPU','GPU','NPU'] verified
- Env: ZE_ENABLE_NPU=1 ZE_ENABLE_VPU_DRIVER=1 ZE_FLAT_DEVICE_HIERARCHY=COMPACT
