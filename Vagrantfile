$pkgs = <<-SHELLP
  dpkg --add-architecture i386
  apt-get update -y #&& apt-get upgrade -y;
  apt-get install -y remmina \
    nuclei \
    i3-wm \
    suckless-tools \
    exploitdb \
    mingw-w64 \
    shellter \
    xclip \
    git \
    wine32
SHELLP

$manual_pkgs = <<-SHELLM
  git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf && ~/.fzf/install --all
  su vagrant -c "git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf && ~/.fzf/install --all"
SHELLM


Vagrant.configure("2") do |config|
  config.vm.box = "kalilinux/rolling";
  #config.ssh.username = "kali";
  config.vm.provider "virtualbox" do |vb|
    vb.name = "KaliVg"
    vb.cpus = "2"
    vb.memory = "5120"
  end

  config.vm.provision "shell", inline: $pkgs;
  config.vm.provision "shell", inline: $manual_pkgs;
  config.vm.provision "file", source: "files/aliases", destination: "/tmp/aliases"
  config.vm.provision "shell", privileged:false, inline: "cat /tmp/aliases >> ~/.zshrc";
  config.vm.provision "file", source: "files/rev64ps", destination: "/tmp/rev64ps"
  config.vm.provision "shell", inline: "cp /tmp/rev64ps /usr/bin/rev64ps && chmod +x /usr/bin/rev64ps";
end
