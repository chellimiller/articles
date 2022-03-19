[See all monorepo articles][monorepos]

# Why use monorepos?

This article writes under the assumption of Node/NPM monorepos.
These concepts also apply to other types of monorepos.

One of the greatest strengths of a monorepo is the ability to create a new package quickly.
I've worked on many projects where I believed a monorepo was unnecessary.
Every single time, this has been a mistake.

## General Benefits

I'm not going to cover what others have in-depth,
but here are some common benefits to monorepos:

1. **Visibility**.
   Code from dependencies is available in a monorepo.
1. **Standardization**.
   Tooling is easier to standardize across projects in a monorepo.
1. **Refactoring**.
   In a monorepo, it is easier to refactor code without causing dependencies to break.
1. **Speed**.
   In a monorepo, bugs in dependencies can be quickly fixed and features can be quickly added.
   Work can begin on a separate branch while the dependency's changes are in code review.
1. **Avoiding Dependency Hell**.
   Versioning can result in attempting to unravel a tangled web of dependencies.
   Having multiple packages in a monorepo with the same version reduces the amount of time spent on versioning.

More information on monorepos:

- [Misconceptions about Monorepos: Monorepo != Monolith](https://blog.nrwl.io/misconceptions-about-monorepos-monorepo-monolith-df1250d4b03c)
- [Wikipedia Article on Monorepos](https://en.wikipedia.org/wiki/Monorepo)

Popular projects that use the monorepo structure:

- [NestJS](https://github.com/nestjs/nest)
- [Angular](https://github.com/angular/angular)
- [React](https://github.com/facebook/react/)
- [Material UI](https://github.com/mui/material-ui)

## Package reusable logic separately

Almost every project contains logic that either is reusable or could easily be made reusable.

In repositories with only one project,
developers will nearly always contain reusable logic in the main application's code.

In a singular repository, extracting code into a separate package would require the following:

1. Creating a separate repository for the reusable code's package
1. Setting up pipelines and other configuration
1. Publishing the package

Any changes to the reusable code needed by the project would require multiple pull requests in multiple repositories.

In early development stages, the process is not economical.
Realistically, reusable code is kept with the project's code.
Problems with this approach are addressed in [Importance of Packaging Reusable Code Separately][reusability].

In a monorepo, creating a separate package is nearly as simple as creating a new folder.
Unlike a new folder, the entire module is a publishable package.

## Add related packages

Beyond reusable code,
different types of projects will have different types of packages that would make sense to include in the same monorepo.

In a standard repository, these packages may never be added even if they are beneficial.

### Libraries

A library project may want the following:

1. Demo and/or documentation app
1. Related libraries to reduce the primary library's scope

### Server Applications

A server application may want the following:

1. Schema and/or types library
1. Demo and/or documentation app
1. Package for accessing its API from a client
1. Package with logic for accessing a database or other server

### Client/Browser Applications

A client application may want the following:

1. UI library
1. User documentation app

[wiki_srp]: https://en.wikipedia.org/wiki/Single-responsibility_principle
[wiki_solid]: https://en.wikipedia.org/wiki/SOLID
[wiki_dry]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
[wiki_di]: https://en.wikipedia.org/wiki/Dependency_inversion_principle
[monorepos]: /../../README.md
[reusability]: /../../monorepos/reusability.md
[why]: /../../monorepos/why.md
