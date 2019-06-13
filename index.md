---
layout: default
---

# LuaProfiler

### Just add one line, you can profiler the Lua code.

### [HOW TO USE]
* Copy the Nvmgo folder under Scripts to the project
* Add code: `[xxlua].DoString(Nvmgo.LuaProfiler.Startup());`  before: `[xxlua].DoString("require('main')");` 
* Run the project, open Windows/Profiler, all the main Lua functions will be displayed inside, the name with a prefix [L]

  [CODE]

  ```
  [xxlua].DoString(Nvmgo.LuaProfiler.Startup());
  [xxlua].DoString("require('main')");
  ```

### [EXAMPLE]
Open Examples/Main.unity, and then open Windows/Profiler to view

### [CONTACT]
Email: nvmgo@foxmail.com