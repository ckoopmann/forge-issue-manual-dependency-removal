# Forge install mechanism broken after manually removing dependency
This repo contains a forge project that is in a state where the `foundry-rs/forge-std` library can neither be removed / updated nor installed sing the respective forge commands.

# How did it get into this state ?

1. Initialize sample project with `forge init`
2. Manually remove the `lib/forge-std` file with `rm lib/forge-std`

# Result

There seems no way to reinstall the manually deleted library again using `forge` commands since: 

1. `forge install foundry-rs/forge-std` fails wtih `A git directory for 'lib/forge-std' is found locally`
2. `forge remove lib/forge-std` fails with `No such dependency`
3. `forge update lib/forge-std` fails with `pathspec 'lib/forge-std' did not match any file(s) known to git`


The only way to resolve this situation seems to be to add the module again using git submodule by running:
`git submodule add --force --name lib/forge-std https://github.com/foundry-rs/forge-std lib/forge-std`

After that the above mentioned forge commands work again as expected.

# Versions
- `forge 0.2.0 (f016135 2022-07-04T00:15:02.930499Z)`
- `git version 2.32.1 (Apple Git-133)`


