# InstantiateDevProject

Julia 1.0.3

    > julia
    > ]activate env

Ok, now try `instantiate`:

    (MyEnv) pkg> instantiate

      Updating registry at `~/.julia/registries/General`
      Updating git-repo `https://github.com/JuliaRegistries/General.git`
     Resolving package versions...
    ERROR: Unsatisfiable requirements detected for package Utils [00000000]:
     Utils [00000000] log:
     ├─Utils [00000000] has no known versions!
     └─restricted to versions * by an explicit requirement — no versions left

fails, as Pkg doesn't know where to find the dev dependency. That's fine, let's
try adding the `Awesomes` dev dependency:

    (MyEnv) pkg> dev dev_projects/Awesomes
     Resolving package versions...
    ERROR: Unsatisfiable requirements detected for package Utils [00000000]:
     Utils [00000000] log:
     ├─Utils [00000000] has no known versions!
     └─restricted to versions * by Awesomes [00000000] — no versions left
       └─Awesomes [00000000] log:
         ├─possible versions are: 0.1.0 or uninstalled
         └─Awesomes [00000000] is fixed to version 0.1.0

doesn't work - Pkg can't find `Utils` dev dependency. Let's try adding that:

    (MyEnv) pkg> dev dev_projects/Utils
     Resolving package versions...
    ERROR: Unsatisfiable requirements detected for package Awesomes [00000000]:
     Awesomes [00000000] log:
     ├─Awesomes [00000000] has no known versions!
     └─restricted to versions * by an explicit requirement — no versions left

this looks like something that should work.
