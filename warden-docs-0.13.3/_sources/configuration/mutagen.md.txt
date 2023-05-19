# Mutagen files syncing

The [mutagen](https://mutagen.io/) can significantly improve the performance of the big projects.
Which contains a huge number of small files on macOS based systems.
For an instance, we can consider the projects which might have a lot of libraries/packages installed
under the `vendor` or `node_modules` directories.
For enabling mutagen on the predefined container,
you just need to assign the container name at the `.env` file,
to the variable `MUTAGEN_CONTAINER_FOR_SYNC`.
For an instance it might look like the following `MUTAGEN_CONTAINER_FOR_SYNC=nuxt-nodejs`.
Also, you need to create syncing rules file, for the mutagen, by the path `.warden/mutagen.yml`.
Such file might look like the following.

```yaml
---
sync:
  defaults:
    mode: two-way-resolved
    watch:
      pollingInterval: 10
    ignore:
      vcs: false
      paths:
        # Root .git folder
        - "/.git/"
        - "/.github/"

        # System files
        - ".DS_Store"
        - "._*"

        # Vim files
        - "*~"
        - "*.sw[a-p]"

        # NodeJS files
        - "/node_modules/**"

        # Optional Project files
        - "/docs/**"
        - "/kubernetes/**"
        - "/packages/**"

    permissions:
      defaultFileMode: "0644"
      defaultDirectoryMode: "0755"

```
