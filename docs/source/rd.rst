Generation of .rd reports
#########################

To generate a HTML or PDF file:
===============================
Generating plots requires the following packages in R:

* `bit64 <https://cran.r-project.org/web/packages/bit64/index.html>`_, (v4.5.2+)
* `tidyverse <https://www.tidyverse.org/>`_, (v2.0.0+)
* `ggExtra <https://cran.r-project.org/web/packages/ggExtra/vignettes/ggExtra.html>`_, (v0.10.1+)
* `plotly <https://plotly.com/r/>`_, (v4.10.4+)
* `data.table <https://github.com/Rdatatable/data.table>`_, (v1.17.8+)
* `cowplot <https://wilkelab.org/cowplot/articles/introduction.html>`_, (v1.2.0+)
* `ggnewscale <https://eliocamp.github.io/ggnewscale/>`_, (v0.5.2+)
* `gridExtra <https://github.com/baptiste/gridextra>`_, (v2.3+)
* `gtable <https://gtable.r-lib.org/>`_, (v0.3.6+)


The packages can be installed in an R console with the following instructions:

.. code-block:: console

   install.packages("bit64", "tidyverse", "ggExtra", "plotly", "data.table", "cowplot", "ggnewscale", "gridExtra", "gtable")

Generating a PDF file requires installing a LaTeX distribution such as TinyTeX. TinyTeX can be installed using the following commands:

.. code-block:: console

   install.packages("tinytex")
   tinytex::install_tinytex()

Please note that only static plots can be rendered in PDF format. **generate_report.sh** will auomatically generate a HTML file if given "-f pdf" and "--interactive" as arguments.

The usage is as follows:

.. code-block:: console

   generate_report.sh -i input1.rd [input2.rd ...] -o output_file [--interactive] [-h]

   Arguments:
   -i, --input     Input rd file(s)
   -o, --output    Output filename (must end in .html or .pdf)
   --interactive   Enable interactive plotting, only supported in html (default: static)
   -h, --help      Show help
