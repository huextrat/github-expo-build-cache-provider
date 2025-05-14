# github-build-cache-provider

A remote build cache provider for [Expo CLI](https://docs.expo.dev/guides/cache-builds-remotely/) that uses GitHub Releases to cache and retrieve build artifacts. This helps speed up local development by reusing builds across machines and CI environments.

## What is this?

This package implements the [Expo Build Cache Provider Plugin interface](https://docs.expo.dev/guides/cache-builds-remotely/) and uses GitHub Releases as a backend for storing and resolving cached builds. When you run `npx expo run:ios` or `npx expo run:android`, the plugin checks if a build with a matching fingerprint exists on GitHub Releases. If found, it downloads and uses the cached build; otherwise, it uploads the new build for future use.

## Installation

Install the provider as a dev dependency:

```sh
yarn add -D github-expo-build-cache-provider
```

## Configuration

Add the following to your Expo project's `app.json`:

```json
{
  "expo": {
    // ...
    "experiments": {
      "remoteBuildCache": {
        "provider": {
          "plugin": "github-expo-build-cache-provider",
          "options": {
            "owner": "<YOUR_GITHUB_USERNAME>",
            "repo": "<YOUR_REPO_NAME>"
          }
        }
      }
    }
  }
}
```

- Replace `<YOUR_GITHUB_USERNAME>` and `<YOUR_REPO_NAME>` with your GitHub username and repository name.

Set your GitHub personal access token (with `repo` permissions) in your environment:

```sh
export GITHUB_TOKEN=ghp_xxxYourTokenHerexxx
```

## Security

- **Never commit your `GITHUB_TOKEN` to source control.**
- Use a token with the minimum required permissions.
- Artifacts are uploaded as GitHub Release assets and are accessible to anyone with access to the repository.

## References

- [Expo Remote Build Cache Providers Documentation](https://docs.expo.dev/guides/cache-builds-remotely/)
- [GitHub Releases Documentation](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases)

---

*This project is not officially affiliated with Expo or GitHub. Use at your own risk.*
