<h3>The steps to signing the chart</h3>

---------------------------------

<h3>note: helm still use gpg old version</h3>
<h4>secring.gpg is public key </h4>
<h4>pubring.kbx is private key </h4>

---------------------------------
- ##### generate public and secret key using GPG
> gpg --full-generate-key

- ##### export the public key:
> gpg --export-secret-keys >~/.gnupg/secring.gpg

- ##### list all key:
> gpg --list-keys

- ##### package chart and signing chart:
> helm package --sign --key duongdx@gmail.com --keyring ~/.gnupg/secring.gpg "chart-directory" -d "repo-directory"

- ##### verify the chart:
> helm verify "repo-directory/chart-version.tgz" --keyring ~/.gnupg/secring.gpg

- ##### verify the chart when install chart:
> helm install --verify --keyring ~/.gnupg/secring.gpg "install_name" "chart_name_alias"

------------------

<h3>Add new chart in repo</h3>

- ##### update index.yaml to chart present
> helm repo index "repo-directory"

- ##### add chart:
> helm repo add "repo-name" "repo-url"
> helm repo add "duongdx-kma" "https://duongdx-kma.github.io/helm-repository/"

- ##### update repo and fetch new chart in repo:
> helm repo update "repo-name"

- ##### search repo and list all versions:
> helm search repo duongdx-kma/socket_chart --versions