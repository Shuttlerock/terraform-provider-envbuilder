---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "envbuilder_cached_image Resource - terraform-provider-envbuilder"
subcategory: ""
description: |-
  The cached image resource can be used to retrieve a cached image produced by envbuilder. Creating this resource will clone the specified Git repository, read a Devcontainer specification or Dockerfile, and check for its presence in the provided cache repo. If any of the layers of the cached image are missing in the provided cache repo, the image will be considered as missing. A cached image in this state will be recreated until found.
---

# envbuilder_cached_image (Resource)

The cached image resource can be used to retrieve a cached image produced by envbuilder. Creating this resource will clone the specified Git repository, read a Devcontainer specification or Dockerfile, and check for its presence in the provided cache repo. If any of the layers of the cached image are missing in the provided cache repo, the image will be considered as missing. A cached image in this state will be recreated until found.



<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `builder_image` (String) The envbuilder image to use if the cached version is not found.
- `cache_repo` (String) (Envbuilder option) The name of the container registry to fetch the cache image from.
- `git_url` (String) (Envbuilder option) The URL of a Git repository containing a Devcontainer or Docker image to clone.

### Optional

- `base_image_cache_dir` (String) (Envbuilder option) The path to a directory where the base image can be found. This should be a read-only directory solely mounted for the purpose of caching the base image.
- `build_context_path` (String) (Envbuilder option) Can be specified when a DockerfilePath is specified outside the base WorkspaceFolder. This path MUST be relative to the WorkspaceFolder path into which the repo is cloned.
- `cache_ttl_days` (Number) (Envbuilder option) The number of days to use cached layers before expiring them. Defaults to 7 days.
- `devcontainer_dir` (String) (Envbuilder option) The path to the folder containing the devcontainer.json file that will be used to build the workspace and can either be an absolute path or a path relative to the workspace folder. If not provided, defaults to `.devcontainer`.
- `devcontainer_json_path` (String) (Envbuilder option) The path to a devcontainer.json file that is either an absolute path or a path relative to DevcontainerDir. This can be used in cases where one wants to substitute an edited devcontainer.json file for the one that exists in the repo.
- `docker_config_base64` (String) (Envbuilder option) The base64 encoded Docker config file that will be used to pull images from private container registries.
- `dockerfile_path` (String) (Envbuilder option) The relative path to the Dockerfile that will be used to build the workspace. This is an alternative to using a devcontainer that some might find simpler.
- `exit_on_build_failure` (Boolean) (Envbuilder option) Terminates upon a build failure. This is handy when preferring the FALLBACK_IMAGE in cases where no devcontainer.json or image is provided. However, it ensures that the container stops if the build process encounters an error.
- `extra_env` (Map of String) Extra environment variables to set for the container. This may include envbuilder options.
- `fallback_image` (String) (Envbuilder option) Specifies an alternative image to use when neither an image is declared in the devcontainer.json file nor a Dockerfile is present. If there's a build failure (from a faulty Dockerfile) or a misconfiguration, this image will be the substitute. Set ExitOnBuildFailure to true to halt the container if the build faces an issue.
- `git_clone_depth` (Number) (Envbuilder option) The depth to use when cloning the Git repository.
- `git_clone_single_branch` (Boolean) (Envbuilder option) Clone only a single branch of the Git repository.
- `git_http_proxy_url` (String) (Envbuilder option) The URL for the HTTP proxy. This is optional.
- `git_password` (String, Sensitive) (Envbuilder option) The password to use for Git authentication. This is optional.
- `git_ssh_private_key_base64` (String, Sensitive) (Envbuilder option) Base64 encoded SSH private key to be used for Git authentication.
- `git_ssh_private_key_path` (String) (Envbuilder option) Path to an SSH private key to be used for Git authentication.
- `git_username` (String) (Envbuilder option) The username to use for Git authentication. This is optional.
- `ignore_paths` (List of String) (Envbuilder option) The comma separated list of paths to ignore when building the workspace.
- `insecure` (Boolean) (Envbuilder option) Bypass TLS verification when cloning and pulling from container registries.
- `remote_repo_build_mode` (Boolean) (Envbuilder option) RemoteRepoBuildMode uses the remote repository as the source of truth when building the image. Enabling this option ignores user changes to local files and they will not be reflected in the image. This can be used to improve cache utilization when multiple users are working on the same repository. (NOTE: The Terraform provider will **always** use remote repo build mode for probing the cache repo.)
- `ssl_cert_base64` (String) (Envbuilder option) The content of an SSL cert file. This is useful for self-signed certificates.
- `verbose` (Boolean) (Envbuilder option) Enable verbose output.
- `workspace_folder` (String) (Envbuilder option) path to the workspace folder that will be built. This is optional.

### Read-Only

- `env` (List of String, Sensitive) Computed envbuilder configuration to be set for the container in the form of a list of strings of `key=value`. May contain secrets.
- `env_map` (Map of String, Sensitive) Computed envbuilder configuration to be set for the container in the form of a key-value map. May contain secrets.
- `exists` (Boolean) Whether the cached image was exists or not for the given config.
- `id` (String) Cached image identifier. This will generally be the image's SHA256 digest.
- `image` (String) Outputs the cached image repo@digest if it exists, and builder image otherwise.
