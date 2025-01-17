---
created_at: '2023-03-21T09:33:04Z'
hidden: false
label_names: []
position: 0
title: Dorado
vote_count: 1
vote_sum: 1
zendesk_article_id: 6623692647951
zendesk_section_id: 360000040076
---

# Description

Dorado is a high-performance, easy-to-use, open source basecaller for
Oxford Nanopore reads.

## <a href="https://github.com/nanoporetech/dorado#features" id="user-content-features" class="anchor"></a>Features

-   One executable with sensible defaults, automatic hardware detection
    and configuration.
-   Nvidia GPUs including multi-GPU with linear scaling.
-   Modified basecalling (Remora models).
-   Duplex basecalling.
-   [POD5](https://github.com/nanoporetech/pod5-file-format) support for
    highest basecalling performance.
-   Based on libtorch, the C++ API for pytorch.
-   Multiple custom optimisations in CUDA and Metal for maximising
    inference performance.

# License and Disclaimer

(c) 2022 Oxford Nanopore Technologies Ltd.

Dorado is distributed under the terms of the Oxford Nanopore
Technologies, Ltd. Public License, v. 1.0. If a copy of the License was
not distributed with this file, You can obtain one
at [http://nanoporetech.com](http://nanoporetech.com/)

.

## Example Slurm script

-   The following Slurm script is a template to run Basecalling on the
    NVIDIA A100 GPUs. We do not recommend running Dorado jobs on CPUs.
-   `--device 'cuda:all'` will automatically pick up the GPU over CPU
-   We are not providing the models as part of the module yet. 

<!-- -->

    #!/bin/bash -e

    #SBATCH --account        nesi12345
    #SBATCH --job-name       dorado
    #SBATCH --gpus-per-node  A100:1
    #SBATCH --mem            6G
    #SBATCH --cpus-per-task  4
    #SBATCH --time           00:10:00
    #SBATCH --output         slurmout.%j.out

    module purge
    module load Dorado/0.3.0

    dorado download --model dna_r10.4.1_e8.2_400bps_hac@v4.1.0

    dorado basecaller dna_r10.4.1_e8.2_400bps_hac@v4.1.0 pod5s/ > calls.sam --device 'cuda:all'
