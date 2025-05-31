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
choco install vagrant vmware-workstation  

#### macOS (avec Homebrew)
brew install vagrant  
brew install --cask vmware-fusion  

#### Linux (Ubuntu/Debian)
sudo apt update  
sudo apt install vagrant  

#### Installer VMware Workstation manuellement

#### Versions testées :
✅ Vagrant 2.3+  
✅ VMware Workstation 17+  
✅ VMware Fusion 13+  

### 🏗️ Architecture
<img width="968" alt="image" src="https://github.com/user-attachments/assets/d7e9681f-8045-44c2-8223-a5adf5bbfaba" />

### ⚡ Installation rapide

#### 1️⃣ Cloner le repository
git clone https://github.com/votre-username/kubernetes-vagrant-cluster.git  
cd kubernetes-vagrant-cluster 

#### 2️⃣ Démarrer le cluster
Créer et démarrer toutes les VMs  
vagrant up  

#### 3️⃣ Se connecter au control plane
vagrant ssh cp1  
kubectl get nodes  

#### Résultat attendu :  
<img width="413" alt="image" src="https://github.com/user-attachments/assets/74f70fc9-a826-4055-896c-8916b7a87d00" />









### 📁 Structure du projet  
### 🛠️ Configuration Vagrant  
### 🔧 Installation Kubernetes  
### ✅ Tests et validation  
### 🎛️ Gestion du cluster  
### 🐛 Dépannage  
### 📚 Ressources  

