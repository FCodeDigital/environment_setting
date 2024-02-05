# Criar um cluster Kubernetes na DigitalOcean

Para iniciar a criaçao é necessário instalar o (kubectl)[https://kubernetes.io/docs/tasks/tools/] e o (doctl)[https://github.com/digitalocean/doctl].

Rodar o comando `doctl auth init` e inserir um (token criado na DigitalOcean)[https://cloud.digitalocean.com/account/api/tokens].
Rodar o comando `doctl kubernetes cluster kubeconfig save [cluster-id]`, que pode ser copiado de dentro do cluster.

# Comandos kubectl

| Comando   |      Descrição             |
|-----------|:--------------------------:|
| kubectl config get-contexts |  Lists your cluster name, user, and namespace |
| kubectl cluster-info |    Display addresses of the control plane and cluster services   |
| kubectl version | Display the client and server k8s version |
| kubectl get nodes | List all nodes created in the cluster |
| kubectl help | Displays commands that help manage your cluster |


# Comandos doctl

| Comando   |      Descrição             |
|-----------|:--------------------------:|
| doctl kubernetes cluster kubeconfig show <cluster-id|cluster-name> |  Show your cluster's kubeconfig YAML |
| doctl kubernetes |    Displays a variety of commands that help manage your cluster via Digitalocean's API   |
