# Cheat sheet

1. Install [Docker](https://www.docker.com/), [VSCode](https://code.visualstudio.com/) and the [Remote Container extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers),

1. Clone this repository

    ```bash
    /> git clone https://github.com/jchomarat/tech3-dev-container-starterkit.git
    ```

1. Open this repository in VSCode

1. Add a folder called `.devcontainer` at the root of your solution

1. In that folder, add a `devcontainer.json` file with the following content

    ```json
    {
        "name": "Tech3-Demo",

        "build": {
            "dockerfile": "Dockerfile"
        },

        "settings": {
            "terminal.integrated.defaultProfile.linux": "bash"
        },

        "extensions": [
            "ms-python.python",
            "ms-python.vscode-pylance",
        ],
        
        "forwardPorts": [],
        
        "remoteUser": "vscode",

        "workspaceMount": "source=${localWorkspaceFolder},target=/workspace,type=bind",
        "workspaceFolder": "/workspace"
    }
    ```
1. Still in the `.devcontainer` folder, add a file called `Dockerfile` with the following content:

    ```Dockerfile
    # You can pick any Debian/Ubuntu-based image.
    FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu-21.04

    ARG USERNAME=vscode

    # Install additional OS packages
    RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
        && apt-get -y install --no-install-recommends sudo curl vim jq wget python3-pip

    RUN pip install requests

    # apt stuff
    RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
        && chmod 0440 /etc/sudoers.d/$USERNAME 

    # Ensure container does not run under root anymore
    USER $USERNAME
    ```
1. Click on the bottom left of VSCode and select `Reoppen in Container`, or

    * For Windows users: SHIFT+CTRL+P and select Remote-Containers: Build Container.
    * For MacOS users: CMD+SHIFT+P and select Remote-Containers: Build Container.
