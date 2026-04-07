# PROVA-TEMPLATE-REPO

Template remoto per Backstage che:

1. genera file base (`fetch:template`)
2. risolve utente GitLab dal token (`gitlab:user:info`)
3. crea la repo GitLab (`publish:gitlab`)
4. registra `catalog-info.yaml` nel Catalog (`catalog:register`)

## File principali

- `template.yaml`
- `skeleton/README.md`
- `skeleton/catalog-info.yaml`

## Come usarlo in Backstage

1. Pubblica questa cartella in un repository GitLab/GitHub.
2. In Backstage vai su `Register existing component`.
3. Inserisci la URL del `template.yaml` del repo, ad esempio:
   - GitLab: `https://gitlab.com/<group>/<repo>/-/blob/main/template.yaml`
   - GitHub: `https://github.com/<org>/<repo>/blob/main/template.yaml`
4. Dopo la registrazione, in `Create` vedrai `Repository GitLab (Remote)`.

## Token e credenziali

Questo template non contiene token hardcoded.

Le action (`gitlab:user:info`, `publish:gitlab`) usano il token lato backend Backstage da:

- `integrations.gitlab[].token` in config
- tipicamente valorizzato con `${GITLAB_TOKEN}` da env del pod
- env del pod caricata da `backstage-secret` in Kubernetes

Quindi il comportamento e' lo stesso del template locale in immagine, ma aggiornabile da repo senza rebuild dell'immagine.
