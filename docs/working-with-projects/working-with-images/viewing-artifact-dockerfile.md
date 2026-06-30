---
title: Viewing Artifact Dockerfile
weight: 70
---

Harbor can display the source Dockerfile for Docker images that have been built with Dockerfile labels.

### Viewing the Dockerfile

When viewing an artifact's detail page, click the **Dockerfile** tab to display the image's source Dockerfile with syntax highlighting, if available.

![dockerfile_tab](../../../img/dockerfile-tab.png)

### Enabling Dockerfile Display

To display the Dockerfile for your images, build them with the `org.opencontainers.image.source` label:

```bash
docker build \
  --label "org.opencontainers.image.source=$(cat Dockerfile)" \
  -t myregistry/myimage:latest \
  .

docker push myregistry/myimage:latest
```

Harbor also supports alternative label keys:
- `com.example.dockerfile`
- `dockerfile`

### No Dockerfile Available

If the Dockerfile tab shows "No dockerfile found", the image was built without storing the Dockerfile source code.

**Options:**
1. Use the **Build History** tab to view the image's construction steps
2. Rebuild the image with a Dockerfile label (see example above)

### CI/CD Integration

Add the Dockerfile label in your build pipeline:

**GitHub Actions:**
```yaml
- name: Build and push
  run: |
    docker build \
      --label "org.opencontainers.image.source=$(cat Dockerfile)" \
      -t ${{ registry }}/myimage:latest \
      .
```

**GitLab CI:**
```yaml
build-image:
  script:
    - docker build --label "org.opencontainers.image.source=$(cat Dockerfile)" -t $CI_REGISTRY_IMAGE:latest .
```
