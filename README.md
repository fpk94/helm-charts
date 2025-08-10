# Helm Charts Repository

This repository hosts a collection of [Helm](https://helm.sh) charts packaged automatically using the [helm/chart-releaser](https://github.com/helm/chart-releaser) GitHub Action.  
The repository is structured so that each chart resides in its own subdirectory under `./charts`, and releases are automatically created when changes are pushed to the `main` branch.

---

## Repository Structure
```
.
├── charts/
│ ├── example-chart-1/
│ │ ├── Chart.yaml
│ │ ├── values.yaml
│ │ └── templates/
│ ├── example-chart-2/
│ │ ├── Chart.yaml
│ │ ├── values.yaml
│ │ └── templates/
│ ...
├── .github/workflows/
│ └── release.yaml # CI workflow for helm/chart-releaser
└── README.md
```

- **charts/** — Each subdirectory is a standalone Helm chart.
- **.github/workflows/** — Contains the CI/CD configuration for packaging and releasing charts.
- **gh-pages branch** — Hosts the Helm repository index (`index.yaml`) and packaged charts for public consumption.

## Add Charts
To add charts, simply add the helm chart subdirectoy in the `/charts` directory and push to main. The release and the updated `index.yaml` are created by the helm chart releaser action. Do not forget to use semantic versioning and testing deployment before pushing to main.

## Using the Helm Repository

Once charts are released, they can be installed by adding this repository as a Helm repository.

### 1. Add the Helm Repository

```bash
helm repo add my-charts https://fpk94.github.io/helm-charts/
helm repo update
```

### 2. Search for Available Charts

```
bash
helm search repo my-charts
```

### 3. Install a Chart

```bash
helm install <release-name> my-charts/<chart-name> \
  --version <chart-version> 
```

- `<release-name>` — Name of the Helm release in your cluster.
- `<chart-name>` — Name of the chart from this repo.
- `<chart-version>` — Specific version you want to install (optional; installs latest if omitted).

### 4. Upgrade an Existing Release

```bash
helm upgrade <release-name> my-charts/<chart-name> \
```

