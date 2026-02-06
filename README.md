# Sidecar: Extensible Out-of-band Signaling for Trustworthy Telephony

Telephone network abuse tactics continue to outpace defenses, motivating new countermeasures that depend on the reliable delivery of authenticated, rich caller identity information to call destinations.

Regulators and network operators seek to introduce new capabilities, such as stronger caller authentication and branded calling, to improve trust in voice communication. Yet the telephone network lacks the agility to support new capabilities and offers no reliable in-band mechanism for delivering the required metadata end-to-end.

In this paper, we present Sidecar, a distributed secure transport system that reliably delivers call metadata across all telephone technologies while cryptographically preserving subscriber and provider confidentiality, enforcing record expiration, and isolating each record so that neither past nor future activity is revealed in case of compromise. 
We formalize secure out-of-band signaling, define its requirements, and construct scalable protocols that realize its functionality, proving their security in the Universal Composability (UC) framework. 

Our prototype evaluation shows that Sidecar incurs low compute and bandwidth costs and adds only a fraction of a second to call setup.

Sidecar retrofits telephony with a secure and extensible transport layer, providing a medium for researchers and industry stakeholders working to mitigate telephone abuse.


## Initial Setup Instructions
We care a lot about the work you must put in to install the run this project. Therefore we thought it would be best to provide you with a script that does all the work for you. The script is called ```prototype.sh``` and is located in the root directory of the project. It will help you set up the project on your local machine.

But before you run the script, we only assume that you already have docker installed on your machine. If you don't have it, please install it now. Docker is a containerization platform that allows you to run applications in isolated environments called containers. It is available for Windows, Mac, and Linux operating systems. You can find the installation instructions for your specific operating system on the official Docker website.

- Install Docker and Docker Compose
- Run ```sudo chmod +x ./prototype && sudo chmod +x -R scripts/``` to make the scripts executable
- Create a copy of ```.env``` file and update the values as per your setup.
- Run ```./prototype.sh build``` to build the Docker images
- Run ```./prototype.sh up``` to start the services


## Jodi Evaluators and Message Stores
- The current setup uses Terraform and Ansible to set up multiple instances of EV and MS on AWS over different zones in the US
- Once the setup is done, ```automation/hosts.yml``` and ```.env``` files are created, which will be used by the proxy
- Command for the setup TODO
```bash
./prototype.sh up
```

## OOB STIR/SHAKEN CPS
- The current setup uses Terraform and Ansible to set up multiple instances of CPSes on AWS over different zones in the US
- Once the setup is done, ```automation/hosts.yml``` and ```.env``` files are created, which will be used by the proxy
- Command for the setup TODO
```bash
./prototype.sh up
```

## Jodi and OOB STIR/SHAKEN proxy
- The proxy is run within a provider's infrastructure
- Clone the repository and copy the ```automation/hosts.yml``` and ```.env``` files over from the cloud setup
- To run the Jodi proxy, run
```bash
docker compose --profile jodi_proxy up -d
```
- To run the OOB SS proxy, run
```bash
docker compose --profile oobss_proxy up -d
```
- Once either of the proxies is running, get the URL of it and provide it to the JIWF.
