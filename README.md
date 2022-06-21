# An alternative way to describe a IALA's G1128 service specification 

You can collaborate on the service-specification.md file for the specification then the repository will turn the file into a nicely-formatted pdf for you.

The up-to-date pdf file can be found at the release page.

## How to work?

*service-specification.md* file in the root is the working document that you need to fill in every sections being required.

The given document template follows the [IALA's G1128 service specification format](https://www.iala-aism.org/product/g1128-specification-e-navigation-technical-services/).

## Release versioning

The version of release is formatted as:
```
format: "${major}.${minor}.${patch}"
```

A commit without a reserved word only impacts to the patch element, i.e., the increament of the last element (patch version) of a version is executed whenever you make a commit.

For updating the minor element, put *(MINOR)* at the end of a commit message.

As well as the minor element, put *(MAJOR)* at the end of a commit message for major versioning updates.

You can read more details about the versioning from [Git-based symantic versioning](https://github.com/PaulHatch/semantic-version) which is used in the GitHub action of this repository.

