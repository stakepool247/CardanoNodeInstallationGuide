---
description: >-
  This is a guide on how to install a Cardano node for people who are interested
  to run their own ADA Staking Pool
---

# Cardano Node 1.34.1 (Stake Pool) installation guide for dummies

{% hint style="success" %}
The guide is updated for **Mainnet** to work with the **latest release: 1.34.1**

**if you are upgrading from a previous version - check the** [**Upgrade guide**](cardano-node-upgrades/upgrade-from-1.30.x-to-1.34.1.md) **below.**&#x20;
{% endhint %}

****

## 📯 Before we start

### Stake pool operator requirements:

* at least **basic knowledge of Linux administration.**
* **ready to update your node** whenever a new release is coming out.
* &#x20;**Ready to learn** new skills :)

## Hardware Requirements&#x20;

* **2-3 Linux servers** (1 block producing node + 1-2  relay nodes)&#x20;
  * **Min 2 vCPU -** 1.6GHz or faster (2GHz or faster for a stake pool or relay)
  * **Min 12GB** of RAM (16GB Recommended)
  * **70 GB** of disk space (Ideally SSD)
  * **Good internet connection** (at least 10Mbps)
* **Offsite PC** (Home PC/server) for your keys (cold storage)
* **Hardware wallet**: Trezor or Ledger **(HIGHLY recommended)**

\
👉  We are going to use Ubuntu as our choice for the OS.\
👉  If you have any questions - join our telegram group: [https://t.me/StakePool247help](https://t.me/StakePool247help) where we have some great **mentors** who are ready to help you!\


This guide is based on the official Cardano Official guide and from our experience. We understand that the information flow is HUGE... and therefore we want to have a place where you can find all the necessary information in setting up your own personal **ADA Staking Pool**.&#x20;

{% hint style="info" %}
To get support, join Cardano Groups:&#x20;

👉  **StakePool247 Support Group:** \
[https://t.me/StakePool247help](https://t.me/StakePool247help)

\
👉  **Cardano Shelley & StakePool Best Practice Workgroup** [**https://t.me/CardanoStakePoolWorkgroup**](https://t.me/CardanoStakePoolWorkgroup)****

****\
****👉  **Cardano Community Tech Support** [**https://t.me/CardanoCommunityTechSupport**](https://t.me/CardanoCommunityTechSupport)****

****\
****👉  **SPOCRA (**_Stake Pool Operator_ Collective Representation _Assembly)_ **forums https://www.spocra.io** \
****
{% endhint %}

