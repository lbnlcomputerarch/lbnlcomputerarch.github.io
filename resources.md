---
layout: page
title: Resources
nav_order: 3
permalink: /resources/
---

## Resources

### Available Tools

See [Adding Tools to Your Environment]({{ '/docs/adding-tools/' | relative_url }}) to add these tools to your environment.

| Resource | Versions |
| -------- | -------- |
| AMD/Xilinx Vitis/Vivado | 2025.2.1, 2025.2, 2025.1.1, 2025.1, 2023.1, 2022.2, 2023.1 |
| ModelSim | SE 2021.1 |

### Available Servers

| Server | OS | CPU | Memory | FPGA |
| ------ | -- | --- | ------ | ---- |
| `rhodey.lbl.gov`<sup>1</sup> | Ubuntu 22.04.5 LTS | 2 x [AMD EPYC 7763 64-Core Processor](https://www.amd.com/en/products/processors/server/epyc/7003-series/amd-epyc-7763.html){:target="_blank"} | 2 TiB | |
| `wmaximoff.lbl.gov` | Ubuntu 20.04.6 LTS | 2 x [Intel Xeon Silver 4216 CPU @ 2.10GHz](https://www.intel.com/content/www/us/en/products/sku/193394/intel-xeon-silver-4216-processor-22m-cache-2-10-ghz/specifications.html){:target="_blank"} | 187 GiB | 1 x [AMD/Xilinx Alveo U250](https://www.amd.com/en/products/accelerators/alveo/u250/a-u250-a64g-pq-g.html){:target="_blank"} |
| `pmaximoff.lbl.gov` | Ubuntu 20.04.6 LTS | 2 x [Intel Xeon Silver 4216 CPU @ 2.10GHz](https://www.intel.com/content/www/us/en/products/sku/193394/intel-xeon-silver-4216-processor-22m-cache-2-10-ghz/specifications.html){:target="_blank"} | 187 GiB | 1 x [AMD/Xilinx Alveo U280](https://www.amd.com/en/products/accelerators/alveo/u250/a-u250-a64g-pq-g.html){:target="_blank"} |

{: .highlight-title }
> Footnotes:
>
> <strong><sup>1</sup>:</strong> Ensure you perform your work in <code>/scratch/USERNAME</code>.

### BXE Cluster

See the official [Berkeley eXtensible Environment (BXE)](https://lbnlbxe.github.io){:target="_blank"} for more information.

| Server | Description | OS | CPU | Memory | FPGA |
| ------ | ----------- | -- | --- | ------ | ---- |
| `bxe.lbl.gov` | Login Node | Debian GNU/Linux 12 (bookworm) | 1 x Virtual CPU | 8 GiB | |
| `srogers.lbl.gov` | Manager VM Host | Ubuntu 24.04.4 LTS | 2 x [Intel(R) Xeon(R) Gold 6326 CPU @ 2.90GHz](https://www.intel.com/content/www/us/en/products/sku/215274/intel-xeon-gold-6326-processor-24m-cache-2-90-ghz/specifications.html){:target="_blank"} | 2 TiB | |
| `wilson.lbl.gov` | Runner FPGA Host | Ubuntu 24.04.4 LTS | 2 x [AMD EPYC 7282 16-Core Processor](https://www.amd.com/en/support/downloads/drivers.html/processors/epyc/epyc-7002-series/amd-epyc-7282.html){:target="_blank"} | 1 TiB | 8 x [AMD/Xilinx Alveo U250](https://www.amd.com/en/products/accelerators/alveo/u250/a-u250-a64g-pq-g.html){:target="_blank"} |
| `vizion.lbl.gov` | Runner FPGA Host | Ubuntu 22.04.5 LTS | 2 x [AMD EPYC 7282 16-Core Processor](https://www.amd.com/en/support/downloads/drivers.html/processors/epyc/epyc-7002-series/amd-epyc-7282.html){:target="_blank"} | 1 TiB | 8 x [AMD/Xilinx Alveo U250](https://www.amd.com/en/products/accelerators/alveo/u250/a-u250-a64g-pq-g.html){:target="_blank"} |

### Other Resources

| Resource | Link |
| -------- | ---- |
| GitLab Repository | [socks.lbl.gov](https://socks.lbl.gov){:target="_blank"} |
| Berkeley eXtensible Environment (BXE) | [lbnlbxe.github.io](https://lbnlbxe.github.io){:target="_blank"} |
| Official CAG Page | [amcr.lbl.gov → CAG](https://amcr.lbl.gov/departments/computer-science-department/cag/){:target="_blank"} |
