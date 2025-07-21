# ⚠️ TROUBLESHOOTING

This document lists common issues users have encountered with Magentic-UI and how to resolve them. 


## 1. 🐳 Docker Not Detected / 🚫 Podman Not Supported

**Error:**  
`Checking if Docker is running...Failed`  
`Docker is not running. Please start Docker and try again.`

**Solution:**  
- Magentic-UI requires Docker Desktop (Windows/Mac) or Docker Engine (Linux).
- Podman and other container engines are **not supported**.
- Make sure Docker is installed and running.

One possible fix for Mac/Ubuntu (especially if using Colima) is by setting environment variable for DOCKER_HOST ([see issue 81](https://github.com/microsoft/magentic-ui/issues/81), thank you to serproqnx) to point to docker.sock:

```bash
export DOCKER_HOST=unix:///home/<your-username>/.docker/desktop/docker.sock
```
**Note**: you might have to adjust the path to point to the correct location of docker.sock.

Another possible fix on Ubuntu if docker is not running is to make sure your user is in the 'docker' group or run with sudo. 

Please read [Linux post-installation steps for Docker Engine
](https://docs.docker.com/engine/install/linux-postinstall/) for more information.

## 2. 🚪 Port 8081 Fails to Start

**Error:**  
`Port 8081 failed to start` or `Address already in use`

**Solution:**  
- Make sure port 8081 is not being used by another application.
- You can change the port with `magentic ui --port <another_port>`.

## 3. 🏗️ Docker Image Pull Fails

**Error:**  
`Pulling docker image...Failed` or similar

**Solution:**  
- Make sure you have a stable internet connection.
- Update Docker to the latest version.
- Check that you have enough disk space.
- Try building the images manually:
  ```bash
  cd docker
  sh build-all.sh
  ```

## 4. 🪟 WSL2 Not Set Up on Windows

**Error:**  
`Docker is not running` or `WSL2 required`

**Solution:**  
- Follow the [For Windows Users](#for-windows-users) section in the README.
- Ensure Docker Desktop is configured to use WSL2.
   - Go to Settings > Resources > WSL Integration
   - Enable integration with your WSL distro


## 5. 🖥️ Browser Cannot Be Operated

**Symptoms:**  
- UI loads, but browser window is blank or unresponsive.

**Solution:**  
- Make sure Docker containers are running (`docker ps`).
- Check firewall settings and ensure required ports are open.
- Try restarting Docker and Magentic-UI.

## 6. 🏔️ Alpine Linux Compatibility

**Issue:**  
- Magentic-UI is not tested on Alpine Linux. Use Ubuntu or Debian for best results.

## 7. 🌐 Running on Remote Servers

**Issue:**  
- UI is not accessible remotely, or browser does not work.

**Solution:**  
- Make sure ports are open and forwarded correctly.
- Check firewall and security group settings.

## 8. 🟪 Magentic Command Not Found

**Issue:**
- Command not found: Magentic
    ```bash
    magentic ui --port 8081
    zsh: command not found: magentic
    ```

**Solution 1**:

- Make sure you have you have activated your virtual environment.
- You can double check by reactivating it and then running the command again:

    ```bash
    deactivate
    source .venv/bin/activate
    magentic ui --port 8081
    ```

**Solution 2**:

- You may have accidentally installed the package named `magentic` instead of ours `magentic-ui`
- Make sure you are running the following command:

  ```bash
  pip install magentic-ui
  ```
  


## 9. ❓ Still Having Issues?

- Double-check all [pre-requisites](#pre-requisites-please-read) in the README.
- Search [GitHub Issues](https://github.com/microsoft/magentic-ui/issues) for similar problems.
- Open a new issue and include:
  1. A detailed description of your problem
  2. Information about your system (OS, Docker version, etc.)
  3. Steps to replicate the issue (if possible)

---

If you have suggestions for this document or find a solution not listed, please submit a pull request! 🙏
