### External maven assembly

This repo is a sample for how to have a staged set of Maven3 projects to build assemblies.

The motivation is that some projects consist of a core project that can be used as a standalone artifact, but certain variations of it need to contain plugins or other extra files.

To allow to layer the assembly process, but not tying the actual maven projects together as module/parents, a third, external and indepedent _assembly_ project is beneficial. Furthermore, with this setup you can have as many public or private assembly projects as you want.

A crucial benefit to this approach is that the actual assembly information on how to assemble the core project (called _server_ in this example) is contained within that project's POM, thus no excessive knowledge about that is done will be leaked to the assembly project.