# RT-Thread SCons build script.
# Builds the core library plus the optional Ed25519 module (RFC 8032,
# SHA-512); the core library's crypto_eddsa_* functions use BLAKE2b instead.
from building import *
import os

cwd = GetCurrentDir()
src = Glob("src/monocypher.c") + Glob("src/optional/monocypher-ed25519.c")
CPPPATH = [os.path.join(cwd, "src"), os.path.join(cwd, "src", "optional")]
group = DefineGroup("monocypher", src, depend=[""], CPPPATH=CPPPATH)
Return("group")
