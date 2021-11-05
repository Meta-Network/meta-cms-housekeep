#Meta-CMS-Housekeep

Regularly clean up task workspaces.

## Motivation

Meta-CMS-BE creates workspace directories (in docker) on the server,
it may not have permission to clean up workspace directories.
We don't want to run Meta-CMS-BE as root,so we created this project to run housekeeping scripts inside a Docker container to clean up workspace directories.

Example

```bash
# Default configuration,dry run
docker run  -it -v /var/tmp/docker-cms-be:/workdir metaio/meta-cms-housekeep /bin/sh dry_run.sh
# Custom WORKSPACE_DIR&MTIME,dry run
docker run  -it -v /var/tmp/docker-cms-be:/workspaces -e META_CMS_TASK_WORKSPACE_DIR="/workspaces" -e META_CMS_TASK_WORKSPACE_MTIME="+14" metaio/meta-cms-housekeep /bin/sh dry_run.sh

# Default configuration,clean
docker run  -it -v /var/tmp/docker-cms-be:/workdir metaio/meta-cms-housekeep /bin/sh clean.sh
# Custom WORKSPACE_DIR&MTIME,clean
docker run  -it -v /var/tmp/docker-cms-be:/workspaces -e META_CMS_TASK_WORKSPACE_DIR="/workspaces" -e META_CMS_TASK_WORKSPACE_MTIME="+14" metaio/meta-cms-housekeep /bin/sh clean.sh
```
