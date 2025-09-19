### Hardware Configuration for Medium to Heavy LLMs

| Component | For 20B Parameter Models | For 80B Parameter Models |
| :--- | :--- | :--- |
| **GPU (Graphics Card)** | **Minimum:** 16 GB of VRAM (e.g., RTX 4080) <br> **Recommended:** 24 GB of VRAM (e.g., RTX 3090, RTX 4090) | **VRAM:** 80 GB or more <br> **Configuration:** Requires a multi-GPU setup to combine VRAM. |
| **GPU Interconnect** | N/A | High-speed links like **NVLink** or a motherboard with **PCIe 4.0/5.0** for efficient communication between GPUs. |
| **CPU (Central Processing Unit)** | A modern, multi-core processor like an **Intel Core i7/i9** or **AMD Ryzen 7/9**. | A modern, multi-core processor like an **Intel Core i7/i9** or **AMD Ryzen 7/9**. |
| **System RAM** | **Minimum:** 16 GB <br> **Recommended:** 32 GB+ | **Minimum:** 16 GB <br> **Recommended:** 32 GB+ |
| **Storage** | **Type:** NVMe SSD is highly recommended for faster loading times. <br> **Capacity:** 500 GB+ of free space. | **Type:** NVMe SSD is highly recommended for faster loading times. <br> **Capacity:** 500 GB+ of free space. |
| **Power Supply** | A high-wattage PSU (850W+) is recommended. | A high-wattage PSU (850W+) is essential for multi-GPU setups. |
| **Cooling** | Robust cooling for the GPU and CPU is important to prevent performance throttling. | Robust cooling for the GPU and CPU is essential to handle the heat from a multi-GPU setup. |
