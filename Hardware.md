
# Q01

```
Installed Physical Memory (RAM) : 64.0 GB
Total Physical Memory: 63.5 GB
Available Physical Memory: 31.3 GB
Total Virtual Memory: 88.5 GB
Available Virtual Memory: 53.0 GB
Page File Space: 25.0 GB
```

Can you explain to me why I see this in Windows 11 and what it means 
from the point of view of the installed RAM? I have a graphic card 
installed on this PC.

---

# ANSWER 01

The difference between **Installed Physical Memory** and **Total Physical Memory** in Windows (`msinfo32`) comes down to how hardware reserves memory at system startup.

**What the two numbers mean:**

* **Installed Physical Memory (64.0 GB):** The exact total amount of physical RAM modules installed in your motherboard slots.
* **Total Physical Memory (63.5 GB):** The actual portion of that 64 GB that is available for Windows and your applications to use as system memory.

---

**Where did the missing ~0.5 GB (500 MB) go?**

Even though you have a dedicated graphics card, small amounts of your total RAM are set aside as **Hardware Reserved Memory**. Typical causes include:

* **Integrated Graphics / iGPU:** Most modern desktop CPUs (Intel Core or AMD Ryzen) include built-in graphics processing on the processor itself. By default, the motherboard BIOS reserves a small chunk of system RAM (often 256 MB to 512 MB) as dedicated video memory (VRAM) for this iGPU, even if a dedicated graphics card is plugged in.
* **BIOS / PCIe Memory Mapping:** System hardware (PCIe controllers, BIOS firmware, motherboard devices) reserves small memory address ranges at boot so the CPU can communicate with internal components.

---

**How to verify or free up this RAM (Optional):**

1. Open **Task Manager** (`Ctrl` + `Shift` + `Esc`), select the **Performance** tab, and click **Memory**.
2. Look at the bottom of the window for **Hardware reserved**. You will likely see ~512 MB listed there.
3. If you want to disable the integrated GPU's memory allocation, restart your PC, enter your motherboard BIOS settings, and locate the display or graphics section to set **Integrated Graphics / iGPU** to **Disabled**.