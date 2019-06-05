# Shiva 2.0 Editor - Example: Binary Modules
Example demonstrating the use of DLL, DYLIB and SO modules inside the ShiVa 2.0 Editor, C++/Lua integration

# Usage of ShiVa 2.0 Editor Binary Modules
1. Copy module binary to:

- Windows: ShiVa 2.0 Editor installation directory root
- Linux: ShiVa 2.0 Editor installation directory root
- Mac: anywhere, but requires absolute path in Lua package.loadlib() call

2. Call library from Lua using code like this:

```lua
------------------------------------------------------------
-- ShiVa 2.0 Editor Binary Module Loader Example script
-- 2017-05-06 Felix Caffier
-- www.shiva-engine.com
------------------------------------------------------------

local p, m = nil
local s = system.getOSType ( )
if s == system.kOSTypeWindows then
    p, m = package.loadlib("libshivaluamodule.dll", "libinit")
elseif s == system.kOSTypeMac then
    p, m = package.loadlib("/absolute/path/libshivaluamodule.dylib", "libinit")
elseif s == system.kOSTypeLinux then
    p, m = package.loadlib("libshivaluamodule.so", "libinit")
end

log.message ( "-- Binary Module Load Start ----------------------" )
log.message ( p )
log.message ( m )
log.message ( "-- Binary Module Load End ------------------------" )

if p == nil then
    log.error ( "shivaluamodule binary could not be loaded, exiting..." )
    return
end

p() -- run libinit
msgbox("This is a message from the editor. Line break check:\nYay! How about umlauts? äöü")
```

# Building Modules
Demo Projects are included for:

- Windows: Visual Studio 2015 (vs140) in C++
- Linux: Code::Blocks (gcc) in C++
- Mac: Xcode 7 (OSX 10.12) in Obj-C++ (.mm)

# Tutorial
A Tutorial for Windows is available here: https://www.shiva-engine.com/shiva-lua-unlocked-pt2-editor-dll-modules/