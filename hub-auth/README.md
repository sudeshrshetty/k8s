# [HUB-AUTH](https://github.com/trustbloc/hub-auth) k8s deployment #


## pre-requisits
* [Minikube](https://minikube.sigs.k8s.io/docs/start/) with ingress addon.
* GNU sed
* (Optional: Gets installed by make) [kustomize](https://kubectl.docs.kubernetes.io/installation/kustomize/).

## Quick Run
* `make all`
* `make deploy-sandbox`

## Cleanup
* `make undeploy-sandbox`
* `make clean`

## options and features
* By default dns domain is `local.trustboc.dev`. To run with different domain (See next), run with: `make DOMAIN=ali.trustbloc.dev`
* Will create an Ingress for external access. When running with unregistered dns domains, create records (/etc/hosts) for:
	- `hub-auth.DOMAIN`
	- `hub-hydra.DOMAIN`
	- `hub-hydra-admin.DOMAIN`
* Will deploy Sandbox HUB-AUTH with [Hydra](https://github.com/ory/hydra), pointing to an already provisioned PostgreSQL specified with `AUTH_MONGODB_URL` and `HYDRA_POSTGRES_DSN`
	- `make deploy AUTH_MONGODB_URL=mongodb://user:pass@mongodb-address:27017 HYDRA_POSTGRES_DSN=postgres://user:pass@host:5432/authresthydra`
* if running `podman` pass `CONTAINER_CMD=podman` as option to make
* Running with none self-signed certificates: place certs into kustomize/hub-auth/overlays/sandbox/certs, then run with: `make setup-no-certs`.
>files:
	- ca.crt
	- tls.crt
	- tls.key
