# SyntroHub CLI

Command-line client for the SyntroHub AI model registry: register models, transfer artifacts with verified checksums, import evaluation evidence, open and review production releases, and run audited lifecycle transitions.

This repository distributes the released package. The source lives in a private repository; releases here carry the built artifact and its checksum.

## Install

Requires Node.js 22 or newer (Linux, macOS, Windows).

npm installs the release straight from its URL:

```sh
npm install -g https://github.com/SyntoMind/syntrohub-cli-dist/releases/download/v2.0.1/syntrohub-cli-2.0.1.tgz
syntrohub --version
```

The package is not on the npm registry; `npm install -g syntrohub-cli` will return 404.

To verify the checksum before installing:

```sh
curl -LO https://github.com/SyntoMind/syntrohub-cli-dist/releases/download/v2.0.1/syntrohub-cli-2.0.1.tgz
curl -LO https://github.com/SyntoMind/syntrohub-cli-dist/releases/download/v2.0.1/syntrohub-cli-2.0.1.tgz.sha256
sha256sum -c syntrohub-cli-2.0.1.tgz.sha256
npm install -g ./syntrohub-cli-2.0.1.tgz
```

```powershell
Invoke-WebRequest -Uri "https://github.com/SyntoMind/syntrohub-cli-dist/releases/download/v2.0.1/syntrohub-cli-2.0.1.tgz" -OutFile syntrohub-cli-2.0.1.tgz
npm install -g .\syntrohub-cli-2.0.1.tgz
```

There is no standalone executable, Chocolatey package or Python SDK for v2.

## Quickstart

```sh
syntrohub config set apiUrl https://registry.example.com
syntrohub login            # device authorization: approve a short code in your browser
syntrohub doctor

syntrohub manifest init    # then set name, framework, type, task and version
syntrohub push acme/classifier --path ./weights --config syntrohub.yaml
syntrohub list --all
syntrohub pull acme/classifier --version 1.0.0 --output ./downloaded
```

Promoting to production is release-bound:

```sh
syntrohub evidence import acme/classifier --version 1.0.0 --run RUN_ID
syntrohub release request acme/classifier --version 1.0.0 --evidence EVIDENCE_ID --card model-card.json
syntrohub release approve acme/classifier RELEASE_ID          # a second admin reviewer
syntrohub lifecycle promote acme/classifier PRODUCTION --release RELEASE_ID --reason "Release approved"
syntrohub jobs list acme/classifier
```

## Documentation

Full documentation, including the command reference, configuration, the release workflow and automation exit codes, is served by your SyntroHub deployment at `/docs`.

`syntrohub commands` prints the whole command tree as JSON for tooling.

## Support and issues

Report problems through your SyntroHub support channel. This repository does not accept pull requests; it exists to distribute the released package.

## License

MIT. See the LICENSE file in the published package.
