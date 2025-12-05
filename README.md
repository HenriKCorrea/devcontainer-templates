# Dev Container Templates

A collection of custom [Dev Container Templates](https://containers.dev/implementors/templates) for common development environments, hosted on GitHub Container Registry.

## Available Templates

This repository contains the following templates:

- **latex-templates** - LaTeX development environment with TeX Live

## Using These Templates

### In VS Code

1. Open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Select **Dev Containers: Add Dev Container Configuration Files...**
3. Choose **Add configuration to user data folder** or **Add configuration to workspace**
4. Select **Show All Definitions...**
5. Enter the following URL:
   - `ghcr.io/henrikcorrea/devcontainer-templates/latex-templates`

### In devcontainer.json

Reference templates directly in your project's `.devcontainer/devcontainer.json`:

```json
{
  "image": "ghcr.io/henrikcorrea/devcontainer-templates/latex-templates:latest"
}
```

## Repository Structure

```
├── src/
│   └── latex-templates/
│       ├── devcontainer-template.json
│       └── .devcontainer/
│           └── devcontainer.json
├── test/
│   └── latex-templates/
│       └── test.sh
└── .github/
    └── workflows/
        ├── release.yaml
        └── test-pr.yaml
```

## For Template Authors

### Creating a New Template

1. Create a new directory in `src/` with your template name
2. Add `devcontainer-template.json` with metadata:
   ```json
   {
     "id": "my-template",
     "version": "1.0.0",
     "name": "My Template",
     "description": "Description of your template",
     "publisher": "HenriKCorrea"
   }
   ```
3. Create `.devcontainer/devcontainer.json` with your configuration
4. Add tests in `test/my-template/test.sh`

### Template Options

Define customizable options in `devcontainer-template.json`:

```json
{
  "options": {
    "version": {
      "type": "string",
      "description": "Select version",
      "proposals": ["latest", "lts"],
      "default": "latest"
    }
  }
}
```

See the [Dev Container Template specification](https://containers.dev/implementors/templates#devcontainer-templatejson-properties) for details.

### Publishing Templates

Templates are automatically published to GHCR when you:

1. Push changes to the `main` branch
2. Run the **Release** workflow manually from the Actions tab

The GitHub Action workflow will:
- Publish each template to `ghcr.io/henrikcorrea/devcontainer-templates/<template-name>`
- Version templates according to `devcontainer-template.json`
- Generate documentation automatically
- Create a pull request with updated README files

### Making Templates Public

By default, packages on GHCR are private. To make them publicly available:

1. Go to `https://github.com/users/HenriKCorrea/packages`
2. Click on your template package
3. Go to **Package settings**
4. Under **Danger Zone**, change visibility to **Public**

### Versioning

Templates follow [semantic versioning](https://semver.org/):
- **MAJOR** version for incompatible changes
- **MINOR** version for new backwards-compatible features  
- **PATCH** version for backwards-compatible fixes

Update the `version` field in `devcontainer-template.json` before publishing.

### Testing Locally

Run tests for a specific template:

```bash
./.github/actions/smoke-test/build.sh <template-id>
./.github/actions/smoke-test/test.sh <template-id>
```

Example:
```bash
./.github/actions/smoke-test/build.sh latex-templates
./.github/actions/smoke-test/test.sh latex-templates
```

### Documentation

Documentation is auto-generated from:
- `devcontainer-template.json` (metadata)
- `NOTES.md` (additional notes, if present)

The generated `README.md` is created automatically by the release workflow.

**Note**: Enable *Allow GitHub Actions to create and approve pull requests* in **Settings > Actions > General > Workflow permissions**.

## Contributing to the Public Index

To make your templates discoverable in VS Code and GitHub Codespaces:

1. Fork [devcontainers/devcontainers.github.io](https://github.com/devcontainers/devcontainers.github.io)
2. Edit `_data/collection-index.yml`
3. Add your collection:
   ```yaml
   - id: henrikcorrea-templates
     name: HenriKCorrea's Dev Container Templates
     url: https://github.com/HenriKCorrea/devcontainer-templates
   ```
4. Submit a pull request

## Resources

- [Dev Container Specification](https://containers.dev/)
- [Template Distribution Spec](https://containers.dev/implementors/templates-distribution/)
- [VS Code Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
- [GitHub Codespaces](https://github.com/features/codespaces)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
