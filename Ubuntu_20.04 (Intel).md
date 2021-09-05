{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "name": "Ubuntu_MacBook_Pro.ipynb",
      "provenance": [],
      "authorship_tag": "ABX9TyOAIbH68J9N5WG3CZEti/wV",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/iacisme/computer_setup/blob/main/Ubuntu_20.04%20(Intel).md\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "jKDVOzIpRcOP"
      },
      "source": [
        "# **Setting up Ubuntu 18.04 on a 2009 MBP**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "QfLFsxCkR6lK"
      },
      "source": [
        "## **Install Required Display and Network Device Drivers**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "S6p2uybFSQ4e"
      },
      "source": [
        "The following instructions come from this website: https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-ubuntu-18-04-bionic-beaver-linux\n",
        "\n",
        "Run the following command in a terminal:\n",
        "\n",
        "```\n",
        "$ sudo ubuntu-drivers autoinstall\n",
        "```\n",
        "\n",
        "Reboot your system:\n",
        "```\n",
        "$ sudo reboot now\n",
        "```"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "wp7eqR4lGYQ_"
      },
      "source": [
        "## **Changing the size of your SWAP file**\n",
        "\n",
        "These instructions are inspired by user posts on the askbuntu forums:https://askubuntu.com/questions/1075505/how-do-i-increase-swapfile-in-ubuntu-18-04"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "TlUxXQMbGtUI"
      },
      "source": [
        "### Steps"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "WfOjOV6wDZVQ"
      },
      "source": [
        "1. Disable the swap file\n",
        "```\n",
        "$ sudo swapoff /swapfile\n",
        "```\n",
        "\n",
        "2. Delete swap file\n",
        "```\n",
        "$ sudo rm  /swapfile\n",
        "```\n",
        "\n",
        "3. Create a new swap file of the desired size, in our case an 8GB one (8G).\n",
        "```\n",
        "$ sudo fallocate -l 8G /swapfile\n",
        "```\n",
        "\n",
        "4. Assign it read/write permissions for root only (not strictly needed, but it tightens security)\n",
        "```\n",
        "$ sudo chmod 600 /swapfile\n",
        "```\n",
        "\n",
        "5. Format the file as swap\n",
        "```\n",
        "$ sudo mkswap /swapfile\n",
        "```\n",
        "\n",
        "6. The file will be activated on the next reboot. If you want to activate it for the current session:\n",
        "```\n",
        "$ sudo swapon /swapfile\n",
        "```\n",
        "\n",
        "7. Reboot\n",
        "```\n",
        "$ sudo reboot now\n",
        "```\n",
        "\n",
        "8. Confirm swapsize change\n",
        "```\n",
        "$ free -h\n",
        "```\n",
        "\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "O7LzCwyMGs9B"
      },
      "source": [
        "## **Setup a Virtual Environment**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "C1wy2I5uVuYe"
      },
      "source": [
        "The instructions below are inspired by the virtual environment set up described here: https://www.pyimagesearch.com/2020/03/25/how-to-configure-your-nvidia-jetson-nano-for-computer-vision-and-deep-learning/\n",
        "\n",
        "Install the following dependancies:\n",
        "\n",
        "```\n",
        "$ sudo apt install -y python3 python3-dev python3-pip\n",
        "```\n",
        "\n",
        "```\n",
        "$ sudo -H pip3 install virtualenv virtualenvwrapper\n",
        "```\n",
        "\n",
        "Add the following lines to **~/.bashrc**, first open it up using vi:\n",
        "\n",
        "```\n",
        "$ sudo vi ~/.bashrc\n",
        "```\n",
        "\n",
        "```\n",
        "# Virtual Env Wrapper Configuration\n",
        "export WORKON_HOME=$HOME/.virtualenvs\n",
        "export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3\n",
        "source /usr/local/bin/virtualenvwrapper.sh\n",
        "```\n",
        "```\n",
        "$ source ~/.bashrc \n",
        "```"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "OIqYBGEdnyWu"
      },
      "source": [
        "## **Create a Virtual Environment**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "S3rTktZ5n5Pa"
      },
      "source": [
        "Create a virtual environment, I'm calling it **\\<env_name>**, where that is any valid name for a venv:\n",
        "\n",
        "```\n",
        "$ mkvirtualenv <env_name> -p python3\n",
        "```\n",
        "\n",
        "If you haven't automatically gone to the virtual environment, you can type this command:\n",
        "\n",
        "```\n",
        "$ workon <env_name>\n",
        "```\n",
        "Here are some other virtual environment commands:\n",
        "\n",
        "\n",
        "* **mkvirtualenv:** Create a Python virtual environment\n",
        "* **lsvirtualenv:** List virtual environments installed on your system\n",
        "* **rmvirtualenv:** Remove a virtual environment\n",
        "* **workon:** Activate a Python virtual environment\n",
        "* **deactivate:** Exits the virtual environment taking you back to your system environment\n",
        "\n",
        "Commands on how to use virtualenv wrapper can be found here: \n",
        "https://virtualenvwrapper.readthedocs.io/en/latest/command_ref.html\n"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "FyOeV83ZtG6p"
      },
      "source": [
        "## **Installing Jupyter Lab**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "5TISLPzXtMjT"
      },
      "source": [
        "The official \"how to\" can be found here: https://jupyter.org/install\n",
        "\n",
        "For my configuration, the official instructions didn't work. \n",
        "\n",
        "**Note**: I installed jupyter lab inside a virtual environment that I had already created. I'm doing it this way because I'm going to have different flavours of jupyter installed so don't want to standard version pushed to all venvs. Besides, I don't know how to do that - yet.\n",
        "\n",
        "This is what I did, inside a virtual environment and was able to run jupyter lab.\n",
        "\n",
        "```\n",
        "$ sudo -H pip3 install jupyter lab\n",
        "```\n",
        "\n",
        "Note, it's a good idea to reboot after installing jupyter.\n",
        "\n",
        "```\n",
        "$ sudo reboot now\n",
        "```"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "2p1DOPqmvbHM"
      },
      "source": [
        "## **Installing nodejs**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "iDYOV0agva47"
      },
      "source": [
        "These instructions come from the following website: https://linuxize.com/post/how-to-install-node-js-on-ubuntu-18.04/\n",
        "\n",
        "To avoid issues with the system installion, make sure you install this inside a virtual env.\n",
        "\n",
        "**You have to replace the `x.x` in the code example below with version you want. As of this writing, the current version is `14.17.1`(LTS). Therefore the `x.x` is going to be replaced by `14.x`.\n",
        "\n",
        "Enable the NodeSource repository by running the following `curl` command as a sudo user:\n",
        "```\n",
        "$ sudo curl -sL https://deb.nodesource.com/setup_x.x | sudo -E bash -\n",
        "```\n",
        "```\n",
        "$ sudo apt-get install -y nodejs\n",
        "```"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "5CuJKICz0vaC"
      },
      "source": [
        "node"
      ],
      "execution_count": null,
      "outputs": []
    }
  ]
}