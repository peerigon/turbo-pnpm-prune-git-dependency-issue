# Turborepo prune pnpm issue
Run:
```sh
 docker build -f apps/web/Dockerfile -t "turbo-prune-example" .
```
and it fails with
```log
 => ERROR [installer  8/11] RUN pnpm install                                                                                                             3.0s
------
 > [installer  8/11] RUN pnpm install:
#19 2.826 Scope: all 5 workspace projects
#19 2.877 Lockfile is up to date, resolution step is skipped
#19 2.884  ERR_PNPM_LOCKFILE_MISSING_DEPENDENCY  Broken lockfile: no entry for 'github.com/peerigon/dashboard-icons/ce27ef933144e09cef3911025f3649040a8571b6' in pnpm-lock.yaml
#19 2.884 
#19 2.884 This issue is probably caused by a badly resolved merge conflict.
#19 2.884 To fix the lockfile, run 'pnpm install --no-frozen-lockfile'.
------
```

Alternative run:
```sh
pnpm turbo prune --scope=web --docker                          
```
and see that 
```yaml
github.com/peerigon/dashboard-icons/ce27ef933144e09cef3911025f3649040a8571b6:
    resolution: {tarball: https://codeload.github.com/peerigon/dashboard-icons/tar.gz/ce27ef933144e09cef3911025f3649040a8571b6}
    name: dashboard-icons
    version: 1.0.0
    dev: false
```
is missing in the `out/pnpm-lock.yaml`