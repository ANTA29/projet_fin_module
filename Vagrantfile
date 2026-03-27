Vagrant.configure("2") do |config|
  # On définit l'image Ubuntu 22.04 pour toutes les machines
  config.vm.box = "ubuntu/jammy64"
  config.vm.provider "vmware_desktop"

  # --- VM 1 : LA PASSERELLE (FIREWALL) ---
  config.vm.define "VM1firewall" do |p|
    p.vm.hostname = "firewall"
    # Réseau DMZ (vers le Web)
    p.vm.network "private_network", ip: "192.168.100.1"
    # Réseau LAN (vers la DB)
    p.vm.network "private_network", ip: "192.168.10.1"
    
    # Commande pour autoriser le passage des données entre les cartes réseau
    p.vm.provision "shell", inline: "sysctl -w net.ipv4.ip_forward=1"
  end

  # --- VM 2 : SERVEUR WEB ---
  config.vm.define "VM2web" do |w|
    w.vm.hostname = "serveur-web"
    w.vm.network "private_network", ip: "192.168.100.10"
    # Route pour que le Web puisse parler à la DB via la passerelle
    w.vm.provision "shell", inline: "ip route add 192.168.10.0/24 via 192.168.100.1"
  end

  # --- VM 3 : SERVEUR BD ---
  config.vm.define "VM3BD" do |d|
    d.vm.hostname = "serveur-db"
    d.vm.network "private_network", ip: "192.168.10.10"
    # Route pour que la DB puisse répondre au Web via la passerelle
    d.vm.provision "shell", inline: "ip route add 192.168.100.0/24 via 192.168.10.1"
  end
end