# application-ontology-template

template repository for starting a PMDCo application ontology. iT comes preconfigured with github workflows using [ontology development kit](https://github.com/INCATools/ontology-development-kit).

## how to use

1. Fork this repository
2. edit [seed/project.yaml](/seed/project.yaml)

```yaml
id: <change here>
title: <ontology title>
github_org: materialdigital
git_main_branch: main
repo: <repo name>
uribase: https://w3id.org/pmd/ao
uribase_suffix: xxx
```

3. push changes and run the seed workflow manually under github actions
4. Put ur ontology work into the \*-edit.owl file in src folder, after pushing changes to the repository the build_with imports workflow will run and integrate your changes into the release types defined
5. Documentation of the application ontology s created via widocu and github pages, when the docs workflow runs
