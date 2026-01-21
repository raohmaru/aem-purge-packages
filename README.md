# AEM Purge Packages

Python command-line utility to clean up outdated Adobe Experience Manager (AEM) package versions. It automatically identifies and removes old package versions while retaining the most recent version of each package.

## Prerequisites

- Python 3.6 or higher

## Installation

1. Clone or download this repository:
   ```bash
   git clone <repository-url>
   cd aem-purge-packages
   ```

2. Install required dependencies:
   ```bash
   pip3 install -r requirements.txt
   ```

3. Verify the installation:
   ```bash
   python3 aem-purge-packages.py -h
   ```

## Usage

**Run against a local AEM instance with default credentials:**

```bash
python3 aem-purge-packages.py
```

This will connect to `localhost:4502` using `admin:admin` credentials and analyze all packages created up to today.

**Connect to a remote AEM instance:**
```bash
python3 aem-purge-packages.py --host author.example.com:4502 -u myuser:mypassword
```

## Command-Line Options

| Option | Description |
|--------|-------------|
| `-h`, `--help` | Show help message and exit |
| `-d DATE`, `--date DATE` | Only consider packages created before this date (format: YYYY-MM-DD) |
| `-f`, `--force` | Skip confirmation prompts before each package deletion |
| `--host HOST` | AEM instance host and port (format: `host:port`, default: `localhost:4502`) |
| `-p PATH`, `--path PATH` | Target a specific package subdirectory (e.g., `adobe` searches `/etc/packages/adobe`) |
| `-u USER`, `--user USER` | AEM credentials (format: `username:password`, default: `admin:admin`) |
| `-v`, `--verbose` | Enable detailed logging output |

## Package Naming Convention

The tool only processes packages that follow this naming pattern:
```
package-name-X.Y.Z.b.zip
```

Where `X.Y.Z.b` represents version numbers (supports up to 4 numeric segments).

Packages not following this convention are ignored for safety.

## Important Notes

⚠️ **Warning**: This tool **deletes** packages without uninstalling them first. The package content remains in the repository, but the package metadata is removed.

⚠️ **Backup**: Always backup your AEM instance before running cleanup operations.

⚠️ **Permissions**: Ensure your user account has sufficient permissions to delete packages in AEM.
