# local-cluster

Minimal, 100% Helm-free local Kubernetes cluster managed with **Kustomize** and **[mise](https://mise.jdx.dev)**:

- **Kind** — multi-node HA local cluster (3 `control-planes` + 3 `workers`)
- **Cilium** — pure CNI, eBPF `kube-proxy` replacement & `NodeIPAM`
- **kgateway** — CNCF Gateway API controller (`shared-gw` + HTTP → HTTPS redirect)
- **cert-manager** — local Root CA & automatic wildcard TLS (`*.k8s.internal`)

Works out of the box on **Linux** (Docker) and **macOS** (OrbStack).

## Usage

```sh
mise trust
mise install
mise run up
```

Other commands:
- `mise run status` — show nodes, gateway, TLS certificates, routes & pods
- `mise run apply` — re-apply root Kustomize manifests
- `mise run hosts` — sync `shared-gw` IP and all `HTTPRoute` hostnames into `/etc/hosts`
- `mise run trust-ca` — trust the local Root CA in the OS trust store (macOS & Fedora)
- `mise run down` — delete the cluster

*(Note on Linux/Fedora: if pods hit `too many open files`, set `fs.inotify.max_user_watches=524288` and `fs.inotify.max_user_instances=512` via `sysctl`.)*
