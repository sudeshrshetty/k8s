# [KMS](https://github.com/trustbloc/kms) k8s deployment #


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
	- `authz-oathkeeper-proxy.DOMAIN`
	- `ops-oathkeeper-proxy.DOMAIN`
	- `vault-kms.DOMAIN`
* Will deploy Sandbox KMS: authz and ops with [oathkeeper](https://github.com/ory/oathkeeper), and vault-kms pointing to an already provisioned MongoDB specified with `MONGODB_URL`
	- `make deploy-with-external-mongodb MONGODB_URL=mongodb://user:pass@mongodb-address:27017`
* if running `podman` pass `CONTAINER_CMD=podman` as option to make
* Running with none self-signed certificates: place certs into kustomize/kms/overlays/sandbox/certs, then run with: `make setup-no-certs`.
>files:
	- ca.crt
	- tls.crt
	- tls.key

## Known issues
* authz-kms fails to start when passing KMS_SECRET_LOCK_KEY_PATH pointing to a non-existing key
