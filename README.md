# 🚀 Kubernetes Cluster avec Vagrant et kubeadm
## 📖 Guide complet pour créer un cluster Kubernetes multi-nœuds avec Vagrant et kubeadm sur Ubuntu 22.04
### 📋 Table des matières
🎯 Vue d'ensemble  
📦 Prérequis  
🏗️ Architecture  
⚡ Installation rapide  
📁 Structure du projet  
🛠️ Configuration Vagrant  
🔧 Installation Kubernetes  
✅ Tests et validation  
🎛️ Gestion du cluster  
🐛 Dépannage  
📚 Ressources  

### 🎯 Vue d'ensemble
Ce projet vous permet de créer automatiquement un cluster Kubernetes production-ready composé de :  
🎛️ 1 Control Plane (cp1) - 4GB RAM, 2 vCPUs  
👷 3 Worker Nodes (w1, w2, w3) - 2GB RAM, 2 vCPUs chacun  
🌐 Réseau Calico CNI pour la communication inter-pods  
🐳 Containerd comme runtime de conteneurs  
🔐 RBAC et politiques de sécurité activées  

### 📦 Prérequis
#### 💻 Système hôte
<img width="523" alt="image" src="https://github.com/user-attachments/assets/ba74dcee-8f51-4e04-becf-b854fff35b2f" />

#### 🛠️ Logiciels requis
#### Windows (avec Chocolatey)
```bash
choco install vagrant vmware-workstation
```
#### macOS (avec Homebrew)
```bash
brew install vagrant
brew install --cask vmware-fusion
```
#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install vagrant
```

#### Installer VMware Workstation manuellement

#### Versions testées :
✅ Vagrant 2.3+  
✅ VMware Workstation 17+  
✅ VMware Fusion 13+  

### 🏗️ Architecture
<img width="968" alt="image" src="https://github.com/user-attachments/assets/d7e9681f-8045-44c2-8223-a5adf5bbfaba" />

### ⚡ Installation rapide

1️⃣ **Cloner le repository**

```bash
git clone https://github.com/votre-username/kubernetes-vagrant-cluster.git
cd kubernetes-vagrant-cluster
```

2️⃣ **Démarrer le cluster**  
Créer et démarrer toutes les VMs :

```bash
vagrant up
```

3️⃣ **Se connecter au control plane**

```bash
vagrant ssh cp1
kubectl get nodes
```

#### Résultat attendu :  
<img width="413" alt="image" src="https://github.com/user-attachments/assets/74f70fc9-a826-4055-896c-8916b7a87d00" />

### 📁 Structure du projet
kubernetes-vagrant-cluster/  
├── 📄 Vagrantfile              # Configuration des VMs  
├── 📄 README.md                # Cette documentation  
├── 📁 scripts/  
│   ├── 🔧 common.sh            # Script commun à tous les nœuds  
│   ├── 🎛️ control-plane.sh     # Script spécifique au control plane  
│   └── 👷 worker.sh            # Script pour les workers  
├── 📁 manifests/  
│   ├── 🌐 calico.yaml          # Configuration Calico CNI  
│   └── 🧪 test-app.yaml        # Application de test  
└── 📁 docs/  
    ├── 🐛 troubleshooting.md   # Guide de dépannage  
    └── 🔧 advanced-config.md   # Configuration avancée  

### 🛠️ Configuration Vagrant
#### 📝 Vagrantfile complet
```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # 🐧 Box Ubuntu 22.04 compatible VMware
  config.vm.box = "generic/ubuntu2204"
  
  # 🔧 Configuration VMware globale
  config.vm.provider "vmware_desktop" do |vmware|
    vmware.vmx["memsize"] = "2048"
    vmware.vmx["numvcpus"] = "2"
  end
  
  # 🔐 Configuration SSH
  config.ssh.insert_key = false
  
  # 🎛️ Control Plane (cp1)
  config.vm.define "cp1" do |cp1|
    cp1.vm.hostname = "cp1"
    cp1.vm.network "public_network", bridge: "vEthernet (WSL)"
    
    cp1.vm.provider "vmware_desktop" do |vmware|
      vmware.vmx["displayName"] = "k8s-cp1"
      vmware.vmx["memsize"] = "4096"     # 4GB pour le control plane
      vmware.vmx["numvcpus"] = "2"
    end
    
    # 🚀 Provisioning du control plane
    cp1.vm.provision "shell", path: "scripts/common.sh"
    cp1.vm.provision "shell", path: "scripts/control-plane.sh"
  end
  
  # 👷 Workers (w1, w2, w3)
  (1..3).each do |i|
    config.vm.define "w#{i}" do |worker|
      worker.vm.hostname = "w#{i}"
      worker.vm.network "public_network", bridge: "vEthernet (WSL)"
      
      worker.vm.provider "vmware_desktop" do |vmware|
        vmware.vmx["displayName"] = "k8s-w#{i}"
        vmware.vmx["memsize"] = "2048"   # 2GB pour les workers
        vmware.vmx["numvcpus"] = "2"
      end
      
      # 🚀 Provisioning des workers
      worker.vm.provision "shell", path: "scripts/common.sh"
      worker.vm.provision "shell", path: "scripts/worker.sh"
    end
  end
end
```




### 🔧 Installation Kubernetes  
### ✅ Tests et validation  
### 🎛️ Gestion du cluster  
### 🐛 Dépannage  
### 📚 Ressources  

