
we can import module A in our current module B and can use the exported services of A in module B.

we can export services and modules both.
1. when we export services present in our provider , other module that imports it can access the exported services. (app module is special module which can use app services in provider without explicitly exporting them.)
2. we can also export the modules that we import 