---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "envbuilder_cached_image Data Source - envbuilder"
subcategory: ""
description: |-
  The cached image data source can be used to retrieve a cached image produced by envbuilder.
---

# envbuilder_cached_image (Data Source)

The cached image data source can be used to retrieve a cached image produced by envbuilder.

## Example Usage

```terraform
data "envbuilder_cached_image" "example" {
  builder_image = "ghcr.io/coder/envbuilder:latest"
  git_url       = "https://github.com/coder/envbuilder-starter-devcontainer"
  cache_repo    = "localhost:5000/local/test-cache"
  extra_env = {
    "ENVBUILDER_VERBOSE" : "true"
  }
}

resource "docker_container" "container" {
  image = envbuilder_cached_image.example.image
  env   = data.envbuilder_image.cached.env
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `builder_image` (String) The builder image URL to use if the cache does not exist.
- `cache_repo` (String) The name of the container registry to fetch the cache image from.
- `git_url` (String) The URL of a Git repository containing a Devcontainer or Docker image to clone.

### Optional

- `cache_ttl_days` (Number) The number of days to use cached layers before expiring them. Defaults to 7 days.
- `extra_env` (Map of String) Extra environment variables to set for the container. This may include evbuilder options.
- `git_password` (String, Sensitive) The password to use for Git authentication. This is optional.
- `git_username` (String) The username to use for Git authentication. This is optional.

### Read-Only

- `env` (List of String) Computed envbuilder configuration to be set for the container.
- `exists` (Boolean) Whether the cached image was exists or not for the given config.
- `id` (String) Cached image identifier
- `image` (String) Outputs the cached image URL if it exists, otherwise the builder image URL is output instead.