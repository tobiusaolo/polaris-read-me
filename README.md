

# Polaris Subnet (Compute-NETUID 49) – README

## Subnet Purpose and Objectives

**Polaris** is a Bittensor subnet designed as a decentralized GPU compute marketplace and management layer. Its primary goal is to **connect miners who have spare GPU resources with the Bittensor network**, enabling those GPUs to be used for AI tasks and other compute-intensive workloads in a trustless environment

Polaris’s **mission** is to be *“the best place on this planet to list your GPUs,”* simplifying how operators join the Bittensor compute network . To achieve this, Polaris offers user-friendly tools to register and manage compute nodes across distributed environments 

Key objectives of the Polaris subnet include: 

- **Decentralized Compute Market:** 
- **Robust Validation:** 
- **Ease of Use and Management:**
- **Seamless Bittensor Integration:** 

## Technical Requirements

Running a Polaris node (either as a miner or validator) requires meeting certain hardware, software, and network prerequisites. Below are the minimum and recommended requirements to ensure stable operation:

- **Operating System:** A Linux environment is required to run Polaris. Native installation on Ubuntu 20.04/22.04 (or other Debian-based distributions) is recommended ([GitHub - Windows 10/11 users can participate via the Windows Subsystem for Linux (WSL2), and macOS users can run a Linux VM or use Docker to emulate a Linux environment  (Polaris’s tools will assist in setting up WSL or Docker on these platforms if needed.)  
- **CPU & RAM:** 64-bit multi-core processor (Intel/AMD) with at least 2–4 cores. A minimum of 8 GB RAM is suggested for miners, with 16 GB or more recommended to handle any additional workloads or Docker overhead. Validators can run with similar CPU/RAM; the processes are not extremely heavy, but more resources improve stability under load.  
- **GPU (Mining Nodes Only):** At least one dedicated **NVIDIA GPU** with CUDA capabilities is required to mine on Polaris (AMD GPUs are currently not officially supported by Bittensor’s mining stack). **Minimum:** NVIDIA GPU with ~4 GB VRAM (e.g. GTX 1660 or RTX 2060). **Recommended:** High-performance GPUs with larger memory – for example, an NVIDIA RTX 3090/4090 or even data-center GPUs like A100/H100 will significantly boost your competitiveness Multiple GPUs can be used to provide more compute, either by running multiple miner instances or a single instance that manages several GPUs (Polaris will detect available GPUs on the host). Ensure NVIDIA drivers are installed on your system. If using Docker containers for tasks, also install the NVIDIA Container Toolkit so that Docker can access your GPU.  
- **Storage:** At least **2 GB of free disk space** is required for Polaris installation and logs . However, if you plan to run large workloads or store datasets on your miner, consider having **50+ GB** available. Additionally, Docker images and environment snapshots can consume extra space; 20 GB is a comfortable minimum to avoid issues. Using an SSD is recommended for faster read/write if datasets or large files are involved.  
- **Network and Connectivity:** A reliable internet connection is essential. **Broadband network with upload/download speeds of 5+ Mbps** (preferably 10 Mbps or higher) and low latency will ensure your node communicates effectively in the network. **Miners must be accessible from the internet**: this typically means having a **public IP address** or properly configured port forwarding. By default, Polaris uses TCP **port 8000** for its API and a range of **SSH ports (e.g., 11000–11002)** for incoming connections. If your miner is behind a router or firewall, you will need to forward these ports to your machine’s local IP so that validators can reach it . A static public IP is ideal; if you have a dynamic IP, using a dynamic DNS service can help maintain connectivity . Validators, on the other hand, initiate connections to miners and therefore can operate from behind NAT without port forwarding (though they still require stable outbound connectivity). In all cases, **keep ports open and firewalls configured** to allow necessary traffic while maintaining security best practices (only open what’s needed, use SSH keys or strong passwords)
- **Software Dependencies:** Polaris requires **Python 3.8+** (Python 3.10 recommended) It also uses **Docker** to manage isolated compute environments, so Docker Engine should be installed and running on your system. Other required software includes **Git** (for cloning repositories) and an **OpenSSH server** (for enabling secure connections between validators and miners). On Debian/Ubuntu, you can install these via apt (e.g., `sudo apt install docker.io git openssh-server`). The Polaris installation process will also install Python packages such as `bittensor`, `bittensor-cli`, and `communex` (a network library) as needed . If running on Windows via WSL, ensure WSL is properly set up and Docker is configured inside the WSL environment 

**Note on GPUs and Drivers:** Polaris itself does not impose specific GPU model requirements, but the **better the GPU, the higher the potential rewards**. Modern NVIDIA GPUs (Turing architecture or newer) have proven effective on Bittensor’s compute tasks. Ensure you have the latest NVIDIA drivers for your GPU installed on the host OS. If miners run tasks inside Docker containers, install the NVIDIA Container Toolkit so containers can utilize the GPU. Finally, it’s recommended to disable any power-saving modes on your GPU and ensure adequate cooling – Polaris will utilize the GPU heavily when serving tasks or benchmarks, so stable performance is key.

## Competitiveness Guidance

**How is performance measured?** In the Polaris subnet, **miners’ performance is evaluated by validators** using a variety of metrics. Validators will securely connect to each miner node and verify its hardware and responsiveness. Factors such as **GPU capability (model and CUDA cores), number of GPUs, available VRAM, network bandwidth, and actual computational throughput** are taken into account. The exact benchmarking process may involve running test jobs or measuring how quickly a miner can perform certain tasks. **Higher-performance miners (e.g., those with powerful GPUs and fast connections) will earn higher scores and thus receive greater rewards**, since the Bittensor consensus rewards contributions proportionally to their value

To remain competitive as a **miner** on Polaris, consider the following guidance:

- **Use High-Performance Hardware:** 
- **Maintain Excellent Uptime and Connectivity:**  
- **Optimize Network Settings:**
- **Stay Updated:** The Bittensor core software and Polaris’s own codebase are actively developed. **Keep your Polaris installation up-to-date** to benefit from optimizations, security patches, and new features. The Polaris CLI provides a convenient update command (`polaris update subnet`) which will pull and apply the latest changes 
- **No Custom Model Training Needed:** Unlike some other Bittensor subnets where miners host AI models that might be fine-tuned or trained to improve answers, Polaris miners are providing raw compute power. This means you **do NOT need to train any neural networks or adjust machine learning models** to succeed on Polaris. 
- **Monitor Your Performance:** Polaris provides built-in monitoring tools. For example, you can run `polaris monitor` to observe your miner’s heartbeat signals and resource usage in real time . Use `polaris logs` to watch the logs for any warnings or errors that might indicate problems ( By keeping an eye on these, you can catch issues early (such as a failing GPU, memory bottleneck, or network dropout) and address them before they impact your standing in the network. Many operators also use external tools (like nvidia-smi, Prometheus/Grafana for system metrics, etc.) to track performance metrics over time.  

For those running a **validator** node on Polaris, competitiveness is less about hardware (validators can run on modest servers since they are not doing heavy GPU tasks themselves) and more about **availability and accuracy**. Validators should remain online continuously to participate in every round of validation – if a validator goes offline frequently, it may miss chances to contribute and earn rewards. Moreover, validators might need to handle multiple SSH sessions or job requests simultaneously when checking miners, so having a reliable machine (multi-core CPU and stable network) is important to not become a bottleneck. Validators are typically appointed in the subnet’s genesis or via governance, and the **number of validators is limited**, so if you are serving as one, make sure to run the node with a professional mindset (similar to running a high-uptime server). Keep the validation software updated and monitor its logs for any signs of desynchronization or issues connecting to miners. 

**Competition and Network Dynamics:** 

## Installation Instructions
### Miner Installation
Setting up a Polaris node is straightforward thanks to the provided installation scripts and tools. You can install both miners and validators using the same process (the role is chosen during runtime). Below are step-by-step instructions to get started:

1. **Prepare the System:** Ensure that your system meets the requirements (see above). On a fresh Ubuntu/Debian Linux server, you should update packages and install Docker, Git, and OpenSSH server. For example, on Ubuntu you might run: 

   ```bash
   sudo apt update && sudo apt upgrade -y 
   sudo apt install -y docker.io git openssh-server curl
   ``` 

   *If you’re on Windows:* Enable WSL2 and install an Ubuntu distribution for it . Then within the Ubuntu/WSL terminal, install Docker and other dependencies as above . *If you’re on macOS:* Make sure Docker Desktop is installed , or set up a Linux VM (VirtualBox + Ubuntu ISO) and proceed in that environment.

2. **Clone the Polaris Repository:** Download the Polaris installer repository from GitHub. In a terminal, run: 

   ```bash
   git clone https://github.com/bigideaafrica/polaris.git 
   cd polaris
   ``` 

   > This repository contains the Polaris Manager script and related setup files. *(Note: the repo name might be `polaris` or `Polaris_go` – use the name exactly as given by the GitHub URL. The above is an example; check the official repo link.)*

3. **Run the Installation Script:** Before running, ensure the script has execute permission: `chmod +x polaris_manager.sh`. Then start the interactive installer with: 

   ```bash
   ./polaris_manager.sh
   ``` 

   This will launch the **Polaris Manager** – a menu-driven setup utility. You will see a text-based menu with options like **Install Polaris, Reinstall, Enter Polaris Environment, Uninstall,** etc. . For a first-time setup, choose **“Install Polaris”**. The script will then:  
   - Check your system for required software (and offer to install missing components, including a specific Python version if needed)  
   - Set up a Python virtual environment and install Polaris dependencies (`bittensor`, `communex`, etc.) in that environment .  
   - Install the Polaris CLI tool itself (as a Python package) .  
   - Assist with Docker setup (ensuring the Docker daemon is running) and any necessary configurations.  
   - Prompt you to input network settings. In particular, it may ask for details to populate a `.env` file with your node’s configuration. For example, you’ll provide the host’s public IP, desired API port (default 8000), an SSH port range (e.g., starting at 11000), and credentials for SSH (username/password) . These are used so Polaris knows how to orchestrate connections. If you’re unsure, you can accept defaults and edit the `.env` later.  
   - Finally, the script will initialize the Polaris environment (setting up systemd services or background processes as needed) and complete the installation.

   Follow all prompts in the installer. In case of any errors, the script will typically inform you of missing prerequisites or misconfigurations so you can address them. For example, if Docker isn’t running, it might remind you to start the Docker service and then let you retry.

4. **Enter the Polaris Environment:** Once installation is successful, you can use the Polaris Manager menu option **“Enter Polaris Environment”** to drop into the Polaris command interface (this may open a new shell where the `polaris` command is available) . Alternatively, if the installer finished without needing a special shell, you can simply use the `polaris` CLI on your regular terminal (ensuring your PATH includes the installed venv binaries). 

   At this point, you should be able to run `polaris --help` to see the available commands and confirm everything is set up correctly . You can also check system status via the menu’s **“Check System Status”** option or by running `polaris status` directly .

5. **Register Your Node:** Before your node can participate in the subnet, it needs to register on the Bittensor network. Run the registration command in the Polaris environment:

   ```bash
   polaris register
   ``` 

   This will initiate an interactive registration process. You’ll be asked to choose a registration type. For most users:  
   - Select **“Bittensor Miner Node”** if you want to directly join the Bittensor subnet as a miner using a Bittensor wallet. You will then be prompted to either create a new Bittensor wallet or use an existing one If you create a new one, make sure to save your wallet name and keys securely.  
   - *(Advanced/optional):* The menu might also show **“Commune Miner Node”** and **“Independent Miner”** options . These relate to alternate registration modes (for example, connecting through a community-run orchestrator or running in a standalone mode). If you don’t know what these are, it’s safe to ignore them and stick with **Bittensor Miner Node** which registers you on the main Polaris subnet. (The **“Polaris Miner Node (Coming Soon)”** option is for a future feature – it can be ignored for now 
   - After choosing Bittensor Miner, you’ll go through wallet setup. Then, you will be asked to select the network: **Mainnet (netuid 49)** or **Testnet (netuid 100)**  For real TAO rewards, select Mainnet; if you just want to test without stakes, you can choose Testnet. Confirm your choice, and Polaris will proceed to register your wallet on that subnet. 

   The registration process will output status logs. If successful, your wallet (public key) is now a registered miner on Polaris. This means it occupies a UID in the subnet and can start contributing/competing.

6. **Start the Polaris Service:** Now you’re ready to launch the actual mining or validating service. Run: 

   ```bash
   polaris start
   ``` 

   The CLI may ask you to **select a mode (Miner or Validator)** if your node is capable of both . Choose **Miner** to begin mining (i.e., offering your GPU for tasks), or **Validator** if you intend to perform validation duties (only do this if you are part of the validator set or have been authorized to run a validator). Upon selection, Polaris will start the appropriate background processes for your role. You should see a Polaris banner and a dashboard summary in the console indicating that services are up . For miners, this includes the heartbeat service that pings the network, and for validators it might include validator-specific routines. The start command will daemonize the services (they continue running in the background). 

   *Example:* After starting, you can run `polaris status` to check that everything is running. The output should confirm the Polaris process is active, along with the heartbeat and any other services, showing their process IDs . If something isn’t running, you may need to troubleshoot (see FAQ below).

7. **Monitor and Manage:** With the node running, you can use Polaris commands to monitor it. Some useful commands:  
   - `polaris logs` – View the live logs from Polaris without attaching a debugger . This is useful to see if your miner is receiving heartbeats or if the validator is reporting any issues.  
   - `polaris monitor` – Launch an interactive monitor (if available) that shows real-time heartbeat signals and system metrics for your miner .  
   - `polaris view-compute` – Show details about the compute resources your node is offering (e.g., it might list your GPUs, their specs, etc., as recognized by Polaris) .  
   - `polaris stop` – Gracefully stop the Polaris services if you need to shut down the miner/validator . Use this before powering off your machine or when you want to temporarily pause participation. You can always start again later.  
   - `polaris update subnet` – Update Polaris to the latest version (as mentioned earlier in competitiveness tips). Typically stops services, updates code, and you can then restart.  
   - `polaris --help` – Display all available subcommands and options for reference .

   The Polaris Manager script menu can also perform some of these actions (like starting, stopping, etc. through a UI), but using the direct `polaris` commands is often more convenient once you’re comfortable.

**Installation Example Summary:** After following the above steps, you might have done something like the following on an Ubuntu machine:

```bash
# System prep (Docker, etc.)
sudo apt update && sudo apt install -y docker.io git openssh-server python3.10 python3-pip

# Clone and run Polaris installer
git clone https://github.com/bigideaafrica/polaris.git
cd polaris
chmod +x polaris_manager.sh
./polaris_manager.sh   # choose "Install Polaris", follow prompts

# Enter environment and register
polaris --help         # verify command works
polaris register       # create or use wallet, register on subnet 33

# Start mining
polaris start          # choose Miner mode if prompted

polaris status         # check status, should show services running
polaris logs           # tail logs to ensure heartbeats are being sent
```

After this, your node is actively participating in the Polaris subnet! 🎉  You can let it run and periodically check your standings on Bittensor stats (e.g., via [taostats.io](https://taostats.io) for netuid 33) or monitor via the CLI.
### Validator Installation 
#### System Requirements

To run a validator node on the **Polaris Cloud Subnet**, ensure your system meets the following requirements:
- **Operating System**: Windows, macOS, or Linux
- **RAM**: Minimum 8 GB
- **Docker**: Installed and running
- **CPU**: Modern multi-core processor (e.g., Intel i5 or AMD Ryzen 5)
- **Python Version**: Python 3.8 or higher
- **TAO Tokens**: At least **1 TAO token** (0.0005 TAO burned during registration)

#### Installation & Setup Guide

Follow the steps below to join and contribute to the **Polaris Cloud Subnet** (NetUID 49) as a **Validator**.

##### Step 1: Create Wallets

Create a **coldkey** and **hotkey** for the **subnet validator wallet**:

```bash
# Install bittensor cli
pip install bittensor-cli==9.1.0 # Use latest or desired version

# Create a coldkey for the validator
btcli wallet new_coldkey --wallet.name <your_wallet_name>

# Create a hotkey for the validator
btcli wallet new_hotkey --wallet.name <your_wallet_name> --wallet.hotkey default
```

##### Step 2: Register Keys

Register your **subnet validator key** to the subnet:

```bash
btcli subnet register --netuid 49 --subtensor.network finney --wallet.name <your_wallet_name> --wallet.hotkey default
```

##### Step 3: Verify Wallet Registration

Check that your key has been successfully registered by running:

```bash
btcli wallet overview --wallet.name <your_wallet_name> --subtensor.network finney
```

##### Step 4: Pull and Run the Validator Docker Image

Pull the Docker image for the Polaris validator:

```bash
docker pull bateesa/polaris-validator
```

Run the validator using the appropriate command for your operating system:

**For macOS/Linux**:
```bash
docker run --rm -it -v ~/.bittensor:/root/.bittensor -e WALLET_NAME=<your_wallet_name> -e WALLET_HOTKEY=default bateesa/polaris-validator
```

**For Windows (Command Prompt)**:
```bash
docker run --rm -it -v C:\Users\YourUsername\.bittensor:/root/.bittensor -e WALLET_NAME=<your_wallet_name> -e WALLET_HOTKEY=default bateesa/polaris-validator
```

**For Windows (PowerShell)**:
```powershell
docker run --rm -it -v ${HOME}/.bittensor:/root/.bittensor -e WALLET_NAME=<your_wallet_name> -e WALLET_HOTKEY=default bateesa/polaris-validator
```
## FAQ (Frequently Asked Questions)

- **Q: Do I need an AI model or to train anything to mine on Polaris?**  
  **A:** No – Polaris is a **compute-focused subnet**, meaning miners provide raw computing power (GPU cycles) rather than serving a machine learning model. You don’t have to train or fine-tune any neural network to compete on Polaris. Your node’s performance is determined by your hardware and how well it runs the subnet’s tasks, not by accuracy of AI responses. This is different from some other subnets where model quality matters. In summary, **hardware > algorithms** on Polaris – keep your GPUs running optimally and you’re set.

- **Q: What kind of rewards will I earn, and how are they given?**  
  **A:** Polaris is integrated into the Bittensor network, so miners earn **TAO**, Bittensor’s native token, as a reward for their contributions. The network’s consensus (Yuma) allocates block rewards to Polaris validators, who then distribute rewards to miners based on the performance scores of each mine . Practically, this means if your miner is consistently providing strong compute service, your Bittensor wallet’s TAO balance will increase over time. You do not earn a separate token – it’s all TAO, maintaining consistency with the rest of the Bittensor ecosystem. (If you’re on testnet, the rewards are test-TAO with no real value, just for experimentation.)

- **Q: What is the difference between a miner and a validator on Polaris? Can I run both?**  
  **A:** In the Bittensor subnet design, **miners** provide the service (in Polaris’s case, GPU compute) and **validators** provide oversight (they verify miners’ work and uphold the blockchain consensus). On Polaris, a miner node will dedicate its GPU to running tasks and responding to validator queries (heartbeats, benchmarks), whereas a validator node will connect to many miners to measure their performance and produce blocks accordingly. **Most participants will be miners.** Validators are typically a limited set of nodes (determined by the subnet governance or genesis). Unless you have been specifically included or elected as a validator, you should run a miner. It’s technically possible to run both on separate machines – one as a validator, one as a miner – but running a validator without authorization won’t be effective. The Polaris software does allow you to start in “Validator” mode, but if you are not recognized as a validator by the network, that instance won’t produce blocks or earn rewards. Therefore, **most users should choose Miner mode**. If you are a genesis validator or official validator operator, follow the provided steps but choose Validator mode when starting, and ensure you have the validator key and identity configured as per the subnet’s requirements.

- **Q: I already have a Bittensor wallet (from another subnet or an earlier version). Can I use that on Polaris?**  
  **A:** Yes, you can use an existing Bittensor wallet to register on Polaris – in fact, the installer will ask if you have one during `polaris register`. If you say yes, you’ll provide the name (and ensure the corresponding hotkey/coldkey files are in place). However, be mindful that some users have reported needing to **regenerate or re-import wallets** for Polaris specificall 】. If the registration process indicates an issue with your wallet or if the wallet was created long ago (with old formats), you can create a fresh wallet through the Polaris CLI. This doesn’t affect your other subnets; you can have multiple wallets. Also note, each wallet on Bittensor is tied to a network (via netuid). If your wallet is already registered on another subnet, it can still register on Polaris independently (as subnets have separate UID spaces). The key point is to **have your wallet’s secret keys available** on the machine (usually in `~/.bittensor/wallets/<walletname>`). If Polaris can’t find or use them, consider regenerating the wallet through the prompts.

- **Q: The installer or `polaris register` is asking about a *Commune* key and COMAI balance. What is this?**  
  **A:** Polaris includes an optional concept called **Commune** – this appears to be a community orchestration layer or alternate network mode. If you choose “Commune Miner Node” during registration, it deals with a **Commune key** and mentions a COMAI balance (which seems to be a separate token or credit system . This path is likely for connecting your node to a community-run system or sidechain that might require a certain balance of a token (COMAI) to participate. For **most users, this is not needed**, and you can ignore the Commune option unless you are specifically joining that community experiment. It’s safe to proceed with **Bittensor Miner Node** registration (which doesn’t involve COMAI) and skip Commune-related questions. The **Independent Miner** option is another advanced mode (possibly to run without any network – for development or local testing). In short, unless you know you need the Commune mode, stick to the default Bittensor registration for Polaris.

- **Q: I completed installation, but my miner doesn’t seem to be getting any rewards or tasks. How do I know it’s working?**  
  **A:** First, check that your miner is **registered and running**: use `polaris status` to ensure the process is active and heartbeats are being sen . The Polaris logs (`polaris logs`) will show periodic heartbeat messages or any incoming requests from validators. In the early stages, you might not “see” tasks running because the system could be in a bootstrap phase or tasks are intermittent. Keep in mind that rewards are not instantaneous – they are distributed over blocks. It might take some time (minutes to hours) for your miner to accumulate noticeable TAO, especially if the network is large and your hardware is average. To verify, you can use the Bittensor CLI or taostats to check your wallet’s stake and rank on subnet 33. For example, `btcli overview --subnet 33 --wallet <yourwallet>` (if using bittensor-cli) can show your stake and other stats. If after some time you see no activity: ensure your **ports are open** (validators might be unable to reach you if, say, port 8000 is blocked – check firewall settings and port forwarding) and that your `.env` has the correct public IP. One common oversight is that the machine’s IP changed (for instance, if on DHCP) – you may need to update the HOST in `.env` and restart Polaris. Another tip: try the **testnet** first (netuid 12) where it’s easier to see if you can get in, as it’s less competitive, then switch to mainnet.

- **Q: My Polaris node fails to start or crashes after a while. What can I do?**  
  **A:** Here are a few troubleshooting steps:  
  - **Check the logs:** Run `polaris logs` to get details on why it stopped. The logs might show Python exceptions, network errors, etc. If you see messages about failing to connect or bind to a port, it could be a networking issue (port in use or blocked). If you see errors about missing modules or similar, the installation might have had an issue – consider re-running the installer’s **Reinstall** option to fix any dependency problem 
  - **Ensure correct Python version:** Polaris is tested with Python 3.10. If you have multiple Python versions, the virtual environment might have been set up with an older version that has issues. The installer usually handles this, but if in doubt, manually create a Python 3.10 venv and install Polaris there.  
  - **Wallet issues:** If the service fails around the time of registration (for example, complaining about keys), you might need to generate a new wallet as mentioned above.  
  - **Update and Reinstall:** Polaris Manager offers a **Reinstall** option which performs a clean setup while preserving your config. This can resolve issues by resetting the environment to a known good stat. Make sure to stop any running Polaris processes before reinstalling.  
  - **WSL specifics:** If running on Windows WSL, make sure you launch Polaris from within the WSL Ubuntu environment (not from Windows directly). Also, WSL networking can sometimes reset after a Windows reboot – verify that your WSL instance still has Docker running and the IP has not changed. Running `polaris status` in WSL will confirm if it’s active or not.  
  - **Hardware stability:** For crashes that occur after running for some time, consider hardware factors – an overheating GPU can cause the miner process (or even the system) to crash. Check GPU temperatures and consider underclocking slightly if it’s running too hot. Also ensure your system isn’t running out of memory (monitor RAM and swap usage). 

  If problems persist, you can seek help from the community. The README suggests checking logs and using the troubleshooting menu option, as well as visiting Polaris documentatio . Community channels like the Bittensor Discord or forum might have a **#subnets** or **#Polaris** channel where you can ask for assistance.

- **Q: Can I run multiple Polaris miners to utilize multiple GPUs or machines?**  
  **A:** Yes. Each Polaris miner is essentially a separate process tied to a Bittensor wallet identity. If you have a multi-GPU rig, you have a couple of options:  
  (a) **Run one Polaris instance that uses all GPUs.** Polaris will detect all available GPUs on the system (for example, via CUDA) and the validators’ benchmarking will recognize the total power. This means a single registered miner could be credited for having multiple GPUs. This approach is simpler (one software instance), but note that Bittensor’s reward mechanism may not perfectly linearize rewards for multiple GPUs under one UID – if one process holds many GPUs, it will perform very well, likely keeping that UID safe in top ranks, but you won’t get “multiple shares” of rewards beyond what one UID can earn.  
  (b) **Run multiple instances (one per GPU)**, each with its own wallet (or sub-wallet). This would register multiple UIDs on the subnet, one per GPU. This can potentially maximize your reward share if the subnet’s design rewards separate identities more, but it comes with overhead: you’ll need to allocate specific GPUs to each instance (using environment variables like `CUDA_VISIBLE_DEVICES` or similar so they don’t overlap) and ensure each has unique ports. This is an advanced setup – you’d basically run each instance in a separate folder or container, each on a different port range (e.g., second miner uses API port 8001 and SSH ports 11003-11005, etc.).  

  For most people, running one instance per machine is sufficient. If you have GPUs on different physical machines, you’ll install Polaris on each machine separately. They can use the **same wallet or different wallets**, it’s up to you. Using the same wallet on multiple miners doesn’t combine their power into one (each will register separately anyway), so generally it’s cleaner to use separate wallets. Just keep track of them! Also remember that each miner needs distinct network ports if behind the same IP. If you’re spreading across multiple machines each with its own public IP, then no port conflicts to worry about.

- **Q: Is there a testnet or sandbox for Polaris where I can try things out?**  
  **A:** Yes. During registration, you had the option to choose **Testnet (netuid 100)** instead of Mainne . This Polaris testnet allows you to run a miner without using real TAO for staking or without competing against the full force of mainnet miners. The testnet is ideal for experimentation: you can see how the software works, whether your node stays connected, etc., and any rewards or penalties there are just test tokens. If you want to switch an already set-up node to testnet, you can run `polaris register` again and select the testnet (you may need a separate wallet for it, e.g., a test wallet). Just note that you cannot be on both mainnet and testnet simultaneously with one instance; it’s one or the other at a time because they use different network IDs. If you do use testnet, be aware that performance may not directly translate to mainnet due to the smaller scale, but it’s a great way to ensure your installation is correct and to get familiar with Polaris operations.

- **Q: How do I update or uninstall Polaris if needed?**  
  **A:** Updating is straightforward – use the CLI command `polaris update subnet` to fetch and apply the latest code update . This will likely stop your node, update the repository (via git pull or pip update), and then you can restart the node. It’s good practice to update periodically, especially if the project announces new releases. For uninstalling, if you used the installer script, there is an **Uninstall Polaris** option in the Polaris Manager menu. This will stop services and attempt to remove all Polaris components (it won’t remove Docker or system packages like Python, but will remove the Polaris-specific files and environments. If you installed manually, you can stop the services (`polaris stop`), then simply delete the repository/venv folder. Also, you might want to remove the entry from your PATH (if any) and any systemd service that was created. The uninstall script should handle most of that. Remember to also **deregister your miner** if you no longer want it on the network – currently, Bittensor will automatically drop miners that stop responding after a certain period, but to be graceful you might use a `btcli unregister` command if one exists (this might be advanced and not necessary; simply stopping the node is fine in practice).

- **Q: Where can I learn more or get support for Polaris?**  
  **A:** Beyond this README, you can refer to the official Polaris documentation (if provided by Big Idea Africa or the maintainers) and the broader Bittensor documentation for subnet . Bittensor’s community forums, Discord, and GitHub discussions are valuable resources. If you encounter issues specific to Polaris, check if the repository has a **Discussions** or **Issues** section and post there. For general questions about how subnets work, the Bittensor docs site has an *Understanding Subnets* sectio. Since Polaris is a community-driven subnet (with Big Idea Africa leading it), they might have announcements or Medium articles out – keep an eye on any links or references in the repo for external resources. Lastly, engaging with other subnet miners can be very insightful; many share tips on hardware tuning, best providers to use for cloud GPUs, etc. The field is evolving quickly, and staying connected will help you remain competitive and informed.

## License

This project is licensed under the **MIT License* . You are free to use, modify, and distribute Polaris’s code in accordance with the MIT terms. Contributions to the project are welcome – feel free to fork the repository and open pull requests for improvements.

---

*Polaris Subnet is an open-source initiative by Big Idea Africa, aiming to democratize access to AI compute. By participating in Polaris, you’re contributing to a more decentralized and accessible future for AI development. We hope this README helped you get started. Happy mining!* 🚀


