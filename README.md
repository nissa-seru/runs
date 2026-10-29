# runs

This repository runs commands against commits of public repositories on GitHub's standard hosted runners. It holds one workflow, `run.yml`, started by `workflow_dispatch` with the commit and the command to run, and nothing runs here on a push.

Each run checks out the commits it's given, sets up Node.js and Bun, each unless the run asks for none, runs an optional setup command and then the command under `bash`, in the first checkout or the directory in it the run names, and uploads what they left as one artifact, kept for a day.

A run's colour on GitHub says whether the runner's own steps worked: checking out, setting up, entering the directory the run names, and uploading. When one fails, the artifact holds what was recorded before it, and no `command.exit`. A setup or command that fails leaves the run green. Whether it passed is in the artifact: `setup.exit` and `command.exit` hold their exit codes, beside their logs and timings. A failed setup stops the run before the command, so its artifact holds no `command.exit` or `output.log`.

The workflow holds no permissions and no secrets, and the repository is public, as is everything a run prints.
