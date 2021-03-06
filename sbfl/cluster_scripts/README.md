This directory includes scripts to run jobs on a Sun Grid cluster.


### generate_killmaps_developer.py

`generate_killmaps_developer.py` script generates all cluster jobs to
run killmap on all Defects4J's faults (either real or artificial).

Requirements:

* DEFECTS4J_HOME - Must point to the Defects4J installation.
* KILLMAP_HOME - Must point to the root directory of Killmap.

Usage:

```
  python generate_killmaps_developer.py <script dir> <data dir>
```

Where `<script dir>` is the directory in which the .sh files will be
written, and `<data dir>` should point to the directory where data
generated by `killmap` will be written.

### generate_pipeline_developer.py, generate_pipeline_evosuite.py, and generate_pipeline_randoop.py

Scripts `generate_pipeline_developer.py`, `generate_pipeline_evosuite.py`,
and `generate_pipeline_randoop.py` generate all cluster jobs to run
the pipeline on developer-based data, evosuite-based data, and
randoop-based data respectively.

Requirements:

* DEFECTS4J_HOME - Must point to the Defects4J installation.
* ANALYSIS_HOME - Must point to the analysis directory of the fault-localization-data repository.

Usage:

```
  python generate_pipeline_developer.py <script dir> <output dir>
```

Where `<script dir>` is the directory in which the .sh files will be
written, and `<data dir>` should point to the directory where coverage
and killmaps are found and scores will be written.

### generate_testgenjobs.py

`generate_testgenjobs.py` script generates all cluster jobs to produce
data for generate test suites.

Requirements:

* DEFECTS4J_HOME - Must point to the Defects4J installation.
* KILLMAP_HOME - Must point to the root directory of Killmap.

Usage:

```
  python generate_testgenjobs.py <script dir> <test dir> <min seed> <max seed> <data dir>
```

where `<script dir>` is the directory in which the .sh files will be
written, `<test dir>` is the directory where the test files (i.e.,
.java files) will be written, `<min seed>` and `<max seed>` are two
integers and represent the seed range in which the tests will be
generated, `<data dir>` should point to the directory where
information about bug detection will be written.

### run_killmap_randoop.sh, and run_killmap_evosuite.sh

`run_killmap_randoop.sh`, and `run_killmap_evosuite.sh` take a
(Randoop or EvoSuite, respectively) generated test suite (generated
for a particular fault) and determines: 1) Whether the test suite
detects the real fault of the corresponding Defects4J's fault; 2) The
list of triggering tests; and 3) The list of fault-related classes.

Requirements:

* D4J_HOME - Must point to the Defects4J installation that is used to checkout, compile, test, etc.
* D4J_TMP_DIR - Set the temporary directory for this script (optional). The default is `/tmp/get_trigger_rel_classes_<process_id_of_this_script>`.

Usage:

```
  bash run_killmap_randoop.sh <test suite archive> <output directory>
```

Each script writes the results of 2) and 3) to `<output directory>`.
They also write a jar archive with all compiled classes of the
generated test suite to the output directory. Each script writes the
following files:

* `<output directory>/<test suite archive>.triggering_tests`
* `<output directory>/<test suite archive>.loaded_classes`
* `<output directory>/<test suite archive>.jar`

Note that if the test suite does not detect the real fault, then 2)
and 3) are skipped and no files are written to the output directory.

