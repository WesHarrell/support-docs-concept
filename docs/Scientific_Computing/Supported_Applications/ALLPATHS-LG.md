---
created_at: '2016-05-05T04:11:49Z'
hidden: true
label_names:
- mahuika
- tier1
- biology
position: 23
title: ALLPATHS-LG
vote_count: 0
vote_sum: 0
zendesk_article_id: 218740578
zendesk_section_id: 360000040076
---

<!-- The above lines, specifying the category, section and title, must be
present and always comprising the first three lines of the article. -->

# Description

ALLPATHS-LG is a short read genome assembler from the Computational
Research and Development group at the Broad Institute.

The ALLPATHS-LG home page is at
<http://www.broadinstitute.org/software/allpaths-lg/blog/>.

# Available modules

## Packages with modules

<table>
<thead>
<tr class="header">
</tr>
</thead>
<tbody>
<tr class="odd">
</tr>
</tbody>
</table>

# Licensing requirements

ALLPATHS-LG is made available at no cost subject to a permissive
open-source licence, the full text of which is available at
<ftp://ftp.broadinstitute.org/pub/crd/ALLPATHS/Release-LG/LICENSE>.

# Example scripts

## Example script for the Pan cluster

    #!/bin/bash -e

    #SBATCH --job-name      ALLPATHS-LG_job
    #SBATCH --account       nesi99999
    #SBATCH --time          01:00:00
    #SBATCH --mem-per-cpu   4G
    #SBATCH --output        ALLPATHS-LG_job.%j.out # Include the job ID in the names
    #SBATCH --error         ALLPATHS-LG_job.%j.err # of the output and error files

    module load ALLPATHS-LG/50041-goolf-1.5.14

    # Arguments are from the basic example in the ALLPATHS-LG documentation; please
    # modify them as necessary
    srun RunAllPathsLG PRE=/assemblies DATA=datadir RUN=rundir SUBDIR=attempt1
