#### QEMU


```bash
# Установка QEMU
$ sudo apt update && upgrade

$ sudo apt install libvirt-daemon
$ sudo apt install qemu-kvm libvirt-daemon-system
$ sudo systemctl enable libvirtd
$ sudo systemctl start libvirtd

$ sudo apt install qemu-kvm qemu

$ sudo apt install virt-manager

# Чтобы запускать ARM, MIPS... -программы прямо под Linux
$ sudo apt-get install qemu-user-static
```

`Ctrl+A затем X (два отдельных нажатия) - Выход из QEMU в терминале`
