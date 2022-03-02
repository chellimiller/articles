[See all monorepo articles][monorepos]

# Importance of Packaging Reusable Code Separately

_Note: This article writes under the assumption of a Node/NPM environment.
The concepts apply to other environments as well._

Almost every project contains logic that either is reusable or could easily be made reusable.

## Improve [separation of responsibilities][wiki_srp]

In software development, the [single-responsibility principle][wiki_srp] is a best practice that is often neglected.
This principle is broken at all levels, including in the development of apps themselves.

Reusable logic in applications results in packages that are larger than necessary.
If logic can be considered "reusable",
then one could argue that it's not a part of the project's responsibility.

The scope of a project may grow,
but it is relatively easy to limit the scope of an individual package.

## Encourage [Dependency Inversion][wiki_di]

Writing tightly coupled code is natural.
This is most obvious with junior developers.
We all start out writing code that makes far more assumptions than are healthy.

When reusable code is broken into a separate package,
it is far easier to enforce [dependency inversion][wiki_di].
This is for a few reasons, including:

1. Dependencies (even peer dependencies) must be specified in the project's `package.json`.
1. New packages change a developer's mindset.
   It is easier for a developer to assume the package is not going to be used in a specific package.

When reusable code exists in a project's source code,
it is easier to write tightly coupled code.
This is for a few reasons, including:

1. All dependencies for the project are immediately available.
   If it's even slightly easier to use them, a developer generally will.
1. The developer assumes the code will be used in the specific project.
   With these assumptions, the code may end up being written in a way that's not reusable at all.

## Reduce [code duplication][wiki_dry] _(and maintenance)_

Reusable code is often code that will be used again.
When this code is intertwined with project's code,
the functionality cannot be easily added to a second project.

As covered in the previous section,
code that could have been reusable is often written in a way where it is not.
When adding similar logic to a second project,
developers may have to sift through the original code to determine what is actually needed.

Even if code was written to follow [SOLID][wiki_solid] principles,
there is still excessive maintenance required:

1. Relevant code from the original repository must be copied to the second.
1. Changes must be made so that the code is applicable to the new project.
1. Tests must be rewritten for the copied code.
1. If bugfixes or features are added, the developers will need to remember to copy the changes over to all relevant locations.

This process is not a problem at first, but over time becomes a burden.
Eventually, small differences in behavior will present themselves between the projects.
This can confuse and frustrate the customer and developer alike.

This is not [DRY][wiki_dry] and increases the chances of differing behavior across applications.

Some developers may advocate for breaking out the reusable code when needed.
In practice, this rarely occurs.
It is easier to push off creating a new package for
reusable code when all a developer needs to do is copy code from one project to another.
If extracting the reusable code ever becomes a priority,
it has already created an expensive burden of maintenance and will require excessive refactors.

Had the reusable code been in a monorepo,
a new package could have been created with little effort.
When the functionality was needed by a new project,
the package could have easily been moved to a separate repository
(or even published from the monorepo if that makes more sense for the project).

## Reduce risk

Many software projects are abandoned.
As customer needs and business goals change, many projects become obsolete.
This is the way of software development and it's a reality we all must face.

Breaking projects into smaller, focused packages reduces the amount of work lost when goals change.
Small packages with limited scopes are more likely to be usable by future projects.
The development of reusable packages will accelerate development over time.

[wiki_srp]: https://en.wikipedia.org/wiki/Single-responsibility_principle
[wiki_solid]: https://en.wikipedia.org/wiki/SOLID
[wiki_dry]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
[wiki_di]: https://en.wikipedia.org/wiki/Dependency_inversion_principle
[monorepos]: ./README.md
[monolith]: ./monolith.md
