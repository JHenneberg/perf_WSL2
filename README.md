# perf_WSL2

How to run `perf` on WSL2

This is heavily based on the comment of [MondayCha](https://gist.github.com/abel0b/b1881e41b9e1c4b16d84e5e083c38a13?permalink_comment_id=4532886#gistcomment-4532886).

Tested with

| wsl2 Linux Kernel | Distribution | is_working? |
| --- | --- | --- |
| `5.15.90.1-microsoft-standard-WSL2 x86_64` | Ubuntu-22.04 | [x] |
| `5.15.90.1-microsoft-standard-WSL2 x86_64` | Ubuntu-20.04 | [x] |

## tl;dr

### Windows

```pwsh
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
wsl --update
wsl --install -d Ubuntu-22.04
```

### WSL2

```bash
sudo apt update
sudo apt upgrade
sudo apt install flex bison 
sudo apt install libdwarf-dev libelf-dev libnuma-dev libunwind-dev \
libnewt-dev libdwarf++0 libelf++0 libdw-dev libbfb0-dev \
systemtap-sdt-dev libssl-dev libperl-dev python-dev-is-python3 \
binutils-dev libiberty-dev libzstd-dev libcap-dev libbabeltrace-dev \
make
git clone https://github.com/microsoft/WSL2-Linux-Kernel --depth 1
cd WSL2-Linux-Kernel/tools/perf
make
sudo cp perf /usr/local/bin
```

## More

### Windows

More [Info](https://learn.microsoft.com/de-de/windows/wsl/install-manual)

* activate WSL and virtual machine functions
  
  ```pwsh
  dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
  dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
  ```

* update WSL
 
  ```pwsh
  wsl --update
  wsl --install -d Ubuntu-22.04
  ```

* install linux distribution (`wsl --list --online` shows all available distributions)
  
  ```pwsh
  wsl --install -d Ubuntu-22.04
  ```

### WSL2

* Update and Upgrade

  `update` rereads all package sources, while `upgrade` brings the installed packages up to the latest available in the package sources.

  ```bash
  sudo apt update
  sudo apt upgrade
  ```

* Installing packages to build `perf`

  ```bash
  sudo apt install flex bison 
  sudo apt install libdwarf-dev libelf-dev libnuma-dev libunwind-dev \
  libnewt-dev libdwarf++0 libelf++0 libdw-dev libbfb0-dev \
  systemtap-sdt-dev libssl-dev libperl-dev python-dev-is-python3 \
  binutils-dev libiberty-dev libzstd-dev libcap-dev libbabeltrace-dev \
  make
  ```

* clone WSL2-Linux-Kernel sources
  ```bash
  git clone https://github.com/microsoft/WSL2-Linux-Kernel --depth 1
  ```

* set current directory to `WSL2-Linux-Kernel/tools/perf`
  ```bash
  cd WSL2-Linux-Kernel/tools/perf
  ```

* build perf from sources
  ```bash
  make
  ```
  
* copy sources to `/usr/local/bin`
  ```bash
  sudo cp perf /usr/local/bin
  ```
