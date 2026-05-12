# application-ontology-template

Template repository for starting a [Platform MaterialDigital (PMD)](https://materialdigital.de) application ontology. Preconfigured with GitHub Actions workflows using the [Ontology Development Kit (ODK)](https://github.com/INCATools/ontology-development-kit).

---

## Quick Start

### 1. Create your repository

Click **Use this template** → **Create a new repository**.

### 2. Configure GitHub settings (one-time)

**GitHub Pages** — Settings → Pages → Build and deployment → Source:
- Set to **Deploy from a branch**
- Branch: `gh-pages` / `(root)`

> This is required for versioned documentation. The docs workflow accumulates version directories on the `gh-pages` branch without overwriting previous releases.

**Actions permissions** — Settings → Actions → General:
- Workflow permissions: **Read and write**
- Enable **Allow GitHub Actions to create and approve pull requests**

### 3. Run the Setup workflow

Actions → **Setup New Ontology** → Run workflow.

Set `id` and `uribase_suffix` — both are usually the same lowercase acronym (e.g. `myont`). The workflow scaffolds `src/ontology/`, commits everything, and opens a pull request.

Review and merge that pull request.

### 4. Build your ontology

Edit the `*-edit.owl` file in `src/ontology/`. Every push to `main` triggers the CI pipeline: quality checks, import refresh, and documentation rebuild.

---

## Releasing

Two equivalent ways to publish a versioned release:

**Option A — workflow dispatch (recommended):**
Actions → **Release Ontology** → Run workflow → enter version (e.g. `1.0.0`).

**Option B — git tag:**
```bash
git tag v1.0.0 && git push origin v1.0.0
```

The release workflow:
1. Builds all serialization artifacts (OWL, TTL, JSON-LD) via ODK
2. Sets `owl:versionIRI` to `<ontbase>/<version>` (e.g. `https://w3id.org/pmd/myont/1.0.0`)
3. Commits artifacts to `main` and creates a `v<version>` git tag
4. Creates a GitHub release with OWL / TTL / JSON-LD attached
5. Triggers a versioned documentation build

Version format: semver without the `v` prefix — `1.0.0`, `2.1.3`, etc.

---

## Versioned Documentation Structure

After each release, GitHub Pages serves:

```text
/                     root index — lists all versions
/dev/                 latest build from main (updated on every push)
/dev/doc/             Widoco HTML — development version
/1.0.0/               semver release (preserved forever)
/1.0.0/doc/           Widoco HTML for v1.0.0
/1.0.0/doc/ontology.ttl
/1.0.0/doc/ontology.owl
```

---

## Permanent URLs via w3id

[w3id.org](https://w3id.org) provides stable, persistent URIs for ontologies. Requests to `https://w3id.org/pmd/<id>` are redirected to your GitHub Pages site via content negotiation.

### Setup steps

1. **Fork** [materialdigital/w3id](https://github.com/materialdigital/w3id).
2. Create the directory `pmd/<id>/` in your fork.
3. Copy [`w3id/.htaccess`](w3id/.htaccess) from this repo into that directory.
4. Replace all `YOUR_ONTOLOGY_ID`, `YOUR_GITHUB_ORG`, and `YOUR_REPO_NAME` placeholders.
5. Open a pull request against the upstream `materialdigital/w3id` repo.

### Content negotiation

The `.htaccess` handles content negotiation automatically:

| Accept header              | Redirects to                   |
| -------------------------- | ------------------------------ |
| `text/html`                | `/index-en.html` (Widoco)      |
| `application/ld+json`      | `/ontology.jsonld`             |
| `application/rdf+xml`      | `/ontology.owl`                |
| `text/turtle`              | `/ontology.ttl`                |
| `application/n-triples`    | `/ontology.nt`                 |
| *(default)*                | `/base_ontology.rdf`           |

Versioned IRIs (`https://w3id.org/pmd/<id>/1.0.0`) resolve to the corresponding versioned directory on GitHub Pages.
