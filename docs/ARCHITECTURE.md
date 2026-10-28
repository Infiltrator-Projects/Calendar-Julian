# Julian Calendar — architecture

This repo owns its calendar algorithm, tests and native package. Common 1.19.80 at dc4aac326964ca4400b6e21851d16eea674040c8 owns the general arithmetic and resource ABI used by this module. The exact Common submodule is built and statically linked, not copied into local Common source files. Release sources include the exact Common snapshot for offline .run builds. Provider and independent accuracy fixtures remain CI gates.
