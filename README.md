### External maven assembly

This repo is a sample for how to have a staged set of Maven3 projects to build assemblies.

The motivation is that some projects consist of a core project that can be used as a standalone artifact, but certain variations of it need to contain plugins or other extra files.

To allow to layer the assembly process, but not tying the actual maven projects together as module/parents, a third, external and indepedent _assembly_ project is beneficial. Furthermore, with this setup you can have as many public or private assembly projects as you want.

A crucial benefit to this approach is that the actual assembly information on how to assemble the core project (called _server_ in this example) is contained within that project's POM, thus no excessive knowledge about what is done will be leaked to the assembly project.

Think of the top-level directories as separate repositories, where plugin will depend on server, but server should not know anything about plugin (except on how to load plugins in general, of course).

_Server_ could be an open source project, released separately, but when combined with _plugin_ it becomes a commercial project due to the way _plugin_ modifies it. You do not want to include knowledge about _plugin_ in _server_, nor do you want to have to perform manual work to build the commercial variant of the artifacts. Ideally you will want to create repeatable builds for the combinations, so you want to track changes to _assembly_. _Assembly_ only knows where _plugin_ should live in the final assembled _server_ artifact, but not assume anything else about how _server_ gets built.

That's what this sample illustrates. _Assembly_ could use a bootstrap pom to perform a SCM checkout, or use git submodules to get its references to the other repositories, but however it is done, at each point in time you can repeat that build without leaking too much information into each of the projects.
