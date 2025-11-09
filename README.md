# Multi-Platform Matrix Build with Artifacts

This repository demonstrates a comprehensive GitHub Actions workflow using matrix build strategies for multi-platform CI/CD pipelines.

## Contact Information

**Email:** 22f3001607@ds.study.iitm.ac.in

## Workflow Overview

This project implements a sophisticated matrix build strategy that runs **13 parallel jobs** across multiple dimensions:

### Matrix Dimensions

1. **Cross-Platform Node.js Builds** (9 jobs)
   - Operating Systems: Ubuntu, macOS, Windows
   - Node.js Versions: 16, 18, 20
   - Total combinations: 3 OS × 3 versions = 9 parallel jobs

2. **Python Version Matrix** (4 jobs)
   - Python Versions: 3.9, 3.10, 3.11, 3.12
   - Platform: Ubuntu Latest

### Features

✅ **Parallel Execution** - All matrix jobs run simultaneously for maximum efficiency

✅ **Artifact Management** - Each job generates and uploads unique build artifacts:
- `build-cf47bfd-linux-node16` through `build-cf47bfd-windows-node20`
- `build-cf47bfd-python3.9` through `build-cf47bfd-python3.12`
- `build-cf47bfd-summary` - Aggregated build summary

✅ **Step Identifier** - Each matrix job includes the required `matrix-cf47bfd` step

✅ **Build Artifacts Content**:
- JSON files with build metadata (timestamp, version, platform, build ID)
- Build logs with detailed information
- Python requirements files
- Comprehensive build summary

### Artifacts Generated

Each matrix job produces artifacts with the prefix `build-cf47bfd-` containing:
- Build output JSON with metadata
- Build logs
- Platform-specific information
- Timestamp and build ID

### Workflow Structure

```yaml
jobs:
  matrix-build:
    strategy:
      matrix:
        os: [ubuntu-latest, macos-latest, windows-latest]
        node-version: [16, 18, 20]
    # Generates 9 artifacts
  
  python-matrix-build:
    strategy:
      matrix:
        python-version: ['3.9', '3.10', '3.11', '3.12']
    # Generates 4 artifacts
  
  summary:
    needs: [matrix-build, python-matrix-build]
    # Generates 1 summary artifact
```

## Getting Started

1. **Fork this repository**
2. **Enable GitHub Actions** in your repository settings
3. **Trigger the workflow** by:
   - Pushing to main/master branch
   - Creating a pull request
   - Manually via workflow_dispatch

## Viewing Results

After the workflow completes:

1. Go to the **Actions** tab
2. Select the latest workflow run
3. Scroll to the **Artifacts** section
4. Download artifacts with prefix `build-cf47bfd-`

## Validation Checklist

- [x] At least 3 successful matrix jobs (13 total)
- [x] At least 3 artifacts with prefix `build-cf47bfd` (14 total)
- [x] All artifacts contain actual content (JSON, logs, metadata)
- [x] At least one step includes identifier `matrix-cf47bfd`
- [x] README.md contains email address

## Artifact Examples

### Node.js Build Artifact
```json
{
  "platform": "linux",
  "os": "ubuntu-latest",
  "nodeVersion": "18",
  "timestamp": "2024-03-20T10:30:45.123Z",
  "buildId": "a1b2c3d4e5f6g7h8",
  "status": "success"
}
```

### Python Build Artifact
```json
{
  "language": "python",
  "version": "3.11",
  "timestamp": "2024-03-20T10:30:50.456Z",
  "python_full_version": "3.11.8 (main, ...)",
  "status": "success"
}
```

## Use Cases

This matrix build pattern is ideal for:
- Cross-platform application testing
- Multi-version compatibility verification
- Library distribution builds
- Integration testing across environments
- Performance benchmarking

## License

MIT License

## Questions?

Contact: your.email@example.com
