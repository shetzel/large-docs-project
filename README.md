This is an sfdx project that contains 10 large docs, each 4 MB.  With this project you can reproduce an issue where trying to deploy the docs results in a `EXCEEDED_MAX_SIZE_REQUEST` error from the Metadata API, but retrieving the same docs there is no `EXCEEDED_MAX_SIZE_REQUEST` error when there should be.  Even deploying 10 more docs of the same size, then trying to retrieve 20 docs will not cause an error from the Metadata API.

Steps to repro:
1. Create a scratch org with an existing devhub.  `sfdx force:org:create -f config/project-scratch-def.json -s -a so1`
1. Deploy docs 1-5 `sfdx force:source:deploy -x package-docs-half1.xml`
1. Deploy docs 6-10 `sfdx force:source:deploy -x package-docs-half2.xml`
1. Try to deploy all docs. It will fail. `sfdx force:source:deploy -x package-docs-all.xml`
1. Try to retrieve all docs. It will succeed when an error should be thrown. `sfdx force:source:retrieve -x package-docs-all.xml`
