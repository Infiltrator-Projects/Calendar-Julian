# Julian Calendar — architecture

This repo owns its calendar algorithm, tests and native package. Common 1.19.81 at a99ef676b0e43c7e645c81756e3fd38be0a54406 owns the general arithmetic and resource ABI used by this module. The exact Common submodule is built and statically linked, not copied into local Common source files. Release sources include the exact Common snapshot for offline .run builds. Provider and independent accuracy fixtures remain CI gates.
