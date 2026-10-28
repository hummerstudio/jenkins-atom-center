# jenkins-atom-center

The default atom center for the `jenkins-atom-runner` Jenkins plugin.

Clients read `index.json` from `main`:

```
https://raw.githubusercontent.com/hummerstudio/jenkins-atom-center/main/index.json
```

Publish an atom with `tools/publish-atom.sh` from `jenkins-atom-plugin`; the script appends the version to
`index.json`, writes the package zip, and (when a key is configured) signs the index with `index.json.sig`.
