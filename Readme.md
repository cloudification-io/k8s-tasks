# Overview

Current repository contains simple exercises to get familiar with Kubernetes

Required tools:
- [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)
- [kustomize](https://kubectl.docs.kubernetes.io/installation/kustomize/)
- [helm](https://helm.sh/docs/intro/install/)
- Any text editor

## Aliases

Some useful aliases that you might encounter

```bash
# ----- kubectl ----------
alias k='kubectl'
alias kdl='kubectl delete'
alias klg='kubectl logs'
alias klf='kubectl logs -f'
alias kaf='kubectl apply -f'
alias kdlf='kubectl delete -f'

# ----- kubectl get ----------
alias kg='kubectl get'
alias kgp='kubectl get pods -o wide'
alias kgd='kubectl get deploy -o wide'
alias kgs='kubectl get svc -o wide'
alias kgn='kubectl get nodes -o wide'

# ----- kubectl describe ----------
alias kd='kubectl describe'
alias kdp='kubectl describe pods'
alias kdd='kubectl describe deploy'
alias kds='kubectl describe svc'
alias kdn='kubectl describe nodes'

# ----- Kubectl config ------
alias kc='kubectl config'
alias kcgc='kubectl config get-contexts'
alias kcuc='kubectl config use-context'

# Usage: `kcdfns rook-ceph` - will set default namespace to 'rook-ceph'
function kcdfns() {
  kcgc | grep '\*'
  kubectl config set-context --current --namespace=$1
  kcgc | grep '\*'
}
```

Install with

```bash
wget https://gist.githubusercontent.com/MaximShepelev/5d4001a660e4fe851b94b093fdd182fe/raw/5b565bf7010dab62549e97272bb7393dd4173a30/gistfile1.txt -O ${HOME}/.bashrc_alises_common
echo "" >> $HOME/.bashrc
echo 'source ~/.bashrc_alises_common' >> $HOME/.bashrc
source $HOME/.bashrc
```

[Source](https://gist.github.com/MaximShepelev/5d4001a660e4fe851b94b093fdd182fe)
