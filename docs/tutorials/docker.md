# Docker Guide

## 1. Install Docker

Before you can run ChronoRoot, you need the Docker Engine installed on your computer.

### Windows Users

1. **Download:** Go to [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop/) and download the installer.
2. **Install:** Run the installer. Ensure the option **"Use WSL 2 instead of Hyper-V"** is checked (this is usually the default and provides better performance).
3. **Start:** Open "Docker Desktop" from your Start menu and wait for the engine to start.

### Linux Users

For the most up-to-date installation instructions specific to your distribution (Ubuntu, Debian, Fedora, CentOS, etc.), please refer to the official Docker documentation:

* **[Official Docker Engine Installation Guide](https://docs.docker.com/engine/install/)**

**Post-Installation (Mandatory):**
After installing Docker, you must configure it to run without `sudo` privileges. If you skip this step, the ChronoRoot commands will fail with "Permission Denied."

Run the following command in your terminal:

```bash
sudo usermod -aG docker $USER

```

*Note: You must log out and log back in (or restart your computer) for this change to take effect.*

### Mac Users

1. **Download:** Go to [Docker Desktop for Mac](https://www.docker.com/products/docker-desktop/).
* *Note: Choose "Apple Chip" for M1/M2/M3 processors, or "Intel Chip" for older Macs.*


2. **Install:** Open the `.dmg` file and drag the Docker icon to your Applications folder.
3. **Start:** Open Docker from your Applications folder.

---

## 2. Install NVIDIA Support (Linux & Windows)

**Crucial for AI Acceleration:** To use the AI segmentation features rapidly, Docker needs access to your NVIDIA GPU.

* **Windows:** Simply ensure your [NVIDIA Drivers](https://www.nvidia.com/Download/index.aspx) are up to date. Docker Desktop handles the rest automatically.
* **Linux:** You must install the **NVIDIA Container Toolkit**. Please follow the official setup guide below, as instructions vary by distribution:
* **[NVIDIA Container Toolkit Installation Guide](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)**



**Verify GPU Support:**
Once configured, run this command to verify that Docker can see your GPU:

```bash
docker run --rm --gpus all nvidia/cuda:11.8.0-base-ubuntu20.04 nvidia-smi

```

---

## 3. Download the ChronoRoot Image

We offer three versions of the image. For most users, we recommend the `latest` tag.

```bash
docker pull ngaggion/chronoroot:latest

```

| Image Tag | Contents | Best For... |
| --- | --- | --- |
| `ngaggion/chronoroot:latest` | App + AI Models + Demo Data | **Standard Users** |
| `ngaggion/chronorootbase:full` | Environment + Demo Data | Developers editing source code |
| `ngaggion/chronorootbase:nodemo` | Minimal Environment | Production/Cluster use |

---

## 4. Launching ChronoRoot

We launch the container using your local User ID so that files created inside Docker (results, CSVs) are owned by **you**, not "root".

### Linux

1. **Enable GUI Access:**
```bash
xhost +local:docker

```


2. **Run the Container:**
Replace `/path/to/your/data` with the actual path to your image folder.
```bash
docker run -it --gpus all \
  -u $(id -u):$(id -g) \
  -v /etc/passwd:/etc/passwd:ro \
  -v /etc/group:/etc/group:ro \
  -v "/path/to/your/data":/DATA/ \
  -e DISPLAY=$DISPLAY \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  --shm-size=8gb \
  ngaggion/chronoroot:latest

```



### Windows (WSL2)

For the Graphical User Interface (GUI) to work on Windows, you must run these commands inside a **WSL2 terminal** (e.g., Ubuntu for Windows), not PowerShell or Command Prompt.

1. **Define your data path:**
Note that `/mnt/c/` corresponds to the `C:\` drive.
```bash
# Example: C:\Users\Name\Images becomes:
MOUNT="/mnt/c/Users/Name/Images"

```


2. **Run the Container:**
```bash
docker run -it --gpus all \
    -u $(id -u):$(id -g) \
    -v /etc/passwd:/etc/passwd:ro \
    -v /etc/group:/etc/group:ro \
    -v "$MOUNT":/DATA/ \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    -v /mnt/wslg:/mnt/wslg \
    -e DISPLAY \
    -e WAYLAND_DISPLAY \
    -e XDG_RUNTIME_DIR \
    -e PULSE_SERVER \
    --shm-size=8gb \
    ngaggion/chronoroot:latest

```



### macOS

> **Warning:** Docker on macOS cannot access the GPU directly. AI segmentation will rely on the CPU and will be significantly slower. However, Screening and Data Analysis tools remain fully functional. You must install [XQuartz](https://www.xquartz.org/) to view the interface.

1. **Configure XQuartz:** Open XQuartz preferences, go to **Security**, and ensure "Allow connections from network clients" is checked. Restart XQuartz.
2. **Run:**
```bash
docker run -it \
    -v "/path/to/your/data":/DATA/ \
    -e DISPLAY=host.docker.internal:0 \
    --shm-size=8gb \
    ngaggion/chronoroot:latest

```



---

## 5. Usage Inside the Container

Once the terminal prompt changes (e.g., `(ChronoRoot) root@container:/app#`), use the following commands:

* **`chronoroot`** : Launch Main Interface.
* **`screening`** : Launch Batch Screening.
* **`segmentation`** : Launch AI Segmentation.

**Where is my data?**
Inside the application, navigate to the **`/DATA/`** folder to find the files you mounted from your computer.

---

## Troubleshooting

* **Permission Denied (Linux):** Did you run `sudo usermod -aG docker $USER`? If not, you must use `sudo` before every docker command.
* **GUI Not Showing:**
    * **Linux:** Ensure you ran `xhost +local:docker` before starting the container.
    * **Windows:** Ensure you are running the command inside a WSL2 terminal and that your Windows version supports WSLg (Windows 10 Build 19044+ or Windows 11).


* **Crashes:** If segmentation crashes on large images, increase the shared memory by changing `--shm-size=8gb` to `--shm-size=16gb`.