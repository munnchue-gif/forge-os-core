## THE FORGE — Complete System Record
### Date: 2026-08-08

### HARDWARE
```
Machine:     MSI Laptop
CPU:         Intel Core Ultra 9 275HX (Arrow Lake)
NPU:         Intel Arrow Lake NPU — PCI 00:0b.0 [8086:ad1d]
GPU:         NVIDIA GeForce RTX 5080 Laptop (dGPU)
iGPU:        Intel Graphics [0x7d67]
NPU device:  /dev/accel/accel0
```

### KERNEL
```
Working:     7.0.0-28-generic (Pop!_OS)
Avoid:       7.0.11 (NVMe corruption bug)
Fallback:    7.0.9
Boot mgr:    systemd-boot
Config:      /boot/efi/loader/loader.conf
             default Pop_OS-current
```

### SOFTWARE STACK
```
OS:          Pop!_OS 24.04 Noble
Python:      3.12
Venv:        ~/the-forge/.venv
OpenVINO:    2026.3.0
NPU Driver:  intel-level-zero-npu 1.35.0
Ollama:      running (qwen2.5-coder:7b, llama3.1:8b)
```

### CRITICAL PACKAGES
```
intel-level-zero-npu    1.35.0
intel-fw-npu            1.35.0
intel-driver-compiler-npu 1.35.0
intel-opencl-icd        24.39
intel-level-zero-gpu    1.3
libze1                  1.17.44  (PINNED/HELD)
libze-intel-gpu1        24.39
```

### THE FIX THAT UNLOCKED NPU
```
Problem:  libze1 missing → NPU invisible
Fix:      sudo apt-get install -y libze1=1.17.44.0-1022~22.04
          sudo apt-mark hold libze1
Verified: ['CPU', 'GPU.0', 'GPU.1', 'NPU']
NPU Driver Version: 1784745579
```

### KEY FILE LOCATIONS
```
Forge root:      ~/the-forge/
Forge engine:    ~/the-forge/forge/fabric/
Venv:            ~/the-forge/.venv/
OpenVINO seat:   forge/fabric/bind/openvino_seat.py
NPU ICD:         /etc/level_zero/icd.d/intel_npu.icd
```

### ENVIRONMENT VARIABLES
```bash
export ZE_ENABLE_NPU=1
export ZE_FLAT_DEVICE_HIERARCHY=COMPACT
export PYTHONPATH="$HOME/the-forge/forge:${PYTHONPATH:-}"
export FORGE_SECRET="<set in .venv/bin/activate>"
```

### ALL BUGS FIXED (decoupled path)
1. Circular import → forge/fabric/types.py (Finding moved here)
2. Unawaited coroutine → asyncio.ensure_future()
3. asyncio not imported → added
4. Lambda await syntax → ensure_future
5. Ledger _entries type → plain class
6. overseer.stats() → property (no ())
7. Finding import → from fabric.types
8. libze1 missing → install + hold
9. stale libze_intel_vpu.so → symlink to npu

### BOOT SEQUENCE
```bash
cd ~/the-forge
source .venv/bin/activate
python3 run_forge.py
```

### NPU VERIFICATION
```bash
python3 -c "
import openvino as ov
c = ov.Core()
print('Devices:', c.available_devices)
print('NPU driver:', c.get_property('NPU', 'NPU_DRIVER_VERSION'))
"
```

### IF NPU DISAPPEARS
```bash
dpkg -l | grep libze1
sudo apt-get install -y libze1=1.17.44.0-1022~22.04
sudo apt-mark hold libze1
ls -la /dev/accel/accel0
cat /etc/level_zero/icd.d/intel_npu.icd
```
