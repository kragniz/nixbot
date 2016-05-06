Nixbot
======

The cutest merge assistant in all of nixpkgs.

This bot will merge pull requests if asked nicely by someone who is listed as a
maintainer for the files the pull request changes.

It reads from a simple JSON file containing each maintainer and a list of the
approximate paths of packages they maintain, something like:

```json
{
    "goibhniu": [
        "pkgs/applications/audio/synthv1/*",
        "pkgs/os-specific/linux/xf86-input-wacom/*",
        "pkgs/development/libraries/frei0r/*",
        "pkgs/applications/audio/fluidsynth/*",
        "pkgs/development/libraries/aubio/*",
        "pkgs/applications/audio/jalv/*",
        "pkgs/applications/audio/sonic-visualiser/*",
        "pkgs/development/tools/selenium/chromedriver/*",
        "pkgs/applications/video/key-mon/*",
        "pkgs/development/libraries/mlt/*",
        "pkgs/servers/http/yaws/*",
        "pkgs/development/libraries/libgig/*",
```

This data was auto generated by the `generate-maintainer-paths` script, which
simply runs `git grep <maintainer name>` and checks the word `maintainer` and
`default.nix` appears on the line. If this bot gets actual usage, this list
should be managed in a more sensible and less hacky way.

With this bot running, if a pull request is submitted that touches a package,
the maintainer for that package may comment "@nixbot merge this please" to have
it merged without that maintainer having commit rights for the entirety of
nixpkgs. Merging is not permitted via this method to contributors who are not
maintainers of the package being modified. This can be seen in action here:
https://github.com/nixbot/nixpkgs-sandbox/pull/9


While this is a simple implementation currently, more complex things such as
hydra or travis integration and requiring more than one vote to merge are
possible.
