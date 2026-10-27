A simple script that searches for commits with a keyword to identify breaking changes, generating a markdown report.

To use the script, you need to pass following parameters:

* repo_path = the path to your repository
* branch = the branch you want to use in the repo entered in repo_path
* start_hash = the start of the range of commits to consider
* end_hash = the end of the range of commits to consider. This is the only optional parameter. If you don't enter it HEAD is going to be used as end_hash

The report is written to `report-dxp.md`.

Example:

    ./pretty-breaking-changes-markdown.py /home/yo/src/liferay-portal-ee master f63d698232b7b620536bb32f854286b132fcc07a 4a2e75e4e6fd4c225db62f303ccc33cdd1782ba4

Add `--only` at the end of the arguments to only keep some of the breaking changes. Each value is either `cms`, which keeps modules that contain a `.lfrbuild-cms-standalone` file at `start_hash` or `end_hash` (e.g. `modules/apps/portal/portal-tika`), or a path prefix like `portal-kernel`. A breaking change is kept if it matches any value. The report is written to `report-cms.md` for `--only cms`, `report-cms-core.md` for `cms` plus path prefixes, and `report-core.md` for path prefixes only. `--cms` is short for `--only cms`.

    ./pretty-breaking-changes-markdown.py /home/yo/src/liferay-portal-ee master f63d698232b7b620536bb32f854286b132fcc07a 4a2e75e4e6fd4c225db62f303ccc33cdd1782ba4 --only cms portal-kernel portal-impl
