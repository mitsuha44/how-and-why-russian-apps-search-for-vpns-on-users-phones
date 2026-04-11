# About this repo

This is automated translation of article from RKS Global. Please visit their website and feel free to share both links.

Link to the original article in Russian: https://rks.global/ru/research/vpn-detection

Link to this translation: https://github.com/mitsuha44/how-and-why-russian-apps-search-for-vpns-on-users-phones/blob/main/README.md

# Full article bellow

## RKS Global

**April 2026**

# How and Why Russian Apps Search for VPNs on Users’ Phones

**An analysis of surveillance in 30 popular Russian Android apps**

---

## Context

Russian authorities intend to require major domestic digital companies to participate in censorship and user surveillance. This became known in early April 2026, when the Ministry of Digital Development, Communications and Mass Media of the Russian Federation held special meetings with the largest Russian internet companies by audience size: Sber, Yandex, VK, Wildberries, Ozon, Avito, X5, and others — more than 20 platforms in total.

According to available information, companies were instructed to restrict access to internet services for users whose devices have VPN enabled by April 15, 2026. Those who fail to comply may face the loss of IT accreditation, benefits, removal from the “whitelist,” and effectively the inability to operate under restricted internet conditions.

Guidelines sent by the Ministry describe stages of checks that apps must perform on user devices. Apps are expected to scan network settings, routing and DNS, detect system-level VPNs and proxies, and analyze user behavior — such as sudden country changes or unusual connection patterns.

Experts believe this level of data collection increasingly resembles spyware disguised as useful services, as it involves access to sensitive technical device information that can be used not only to detect configurations but also to deanonymize users. This data is expected to be shared with Roskomnadzor to help identify VPN services that have not yet been blocked.

Authorities are also requiring companies not only to monitor users but to penalize those using VPNs — degrading service quality or restricting access to push users away from circumvention tools. This effectively delegates censorship from the state to private companies, forcing them to bear development costs, legal risks, false positives, and customer loss.

As early as April 7, 2026, users in Russia reported issues accessing Wildberries, Ozon, and VkusVill while using VPNs: slow loading, unavailable product pages, or full service disruption. Previously, services only warned about “incorrect operation with VPN,” but now actively restrict access.

Digital censorship in Russia is entering a new phase. Experts describe a shift from passive to active censorship. Since 2012, blocking was carried out by authorities through blacklists and later automated systems (TSPU). Now, additional data is collected directly from user devices to inform blocking decisions.

---

## Hypothesis

RKS Global previously studied how the MAX messenger detects active VPN connections on Android and sends this data to developers cooperating with Russian law enforcement. VPN providers have already experienced server IP blocking linked to such reports.

Given government pressure and early success, experts hypothesize that many Russian apps will begin detecting VPN usage and reporting it to regulators. This method is highly effective and likely to expand.

The hypothesis: not only MAX, but potentially any Russian Android app may monitor devices for VPN usage, with deep system access and extensive data collection — possibly exceeding official requirements.

---

## Methodology

Experts analyzed 30 of the most popular Russian Android apps to determine what VPN-related data they collect and the extent of surveillance.

Selection was based on MAU (Monthly Active Users), using data from Mediascope (Dec 2025–Feb 2026), RuStore download rankings, company reports (Sber, VK, Ozon, 2GIS), and media publications.

Analysis method:

* Static APK analysis (decompilation via apktool and jadx)
* Search across 68 tracking indicators in 12 surveillance categories
* APK versions from RuStore and Google Play (April 2026)

Limitation: only static analysis was performed (no runtime testing).

---

## Findings

### 1. Apps that track VPN usage

Out of 30 apps:

* **22 detect VPN**
* **19 send VPN status to servers**

These include:
Yandex Browser, Yandex Maps, VKontakte, My MTS, Sberbank Online, T-Bank, VK Video, Wildberries, Kinopoisk, Ozon, Samokat, RuStore, VTB Online, Yandex Music, Avito, Alfa-Bank, 2GIS, MegaMarket, Odnoklassniki, MAX, Rutube, VK Music.

When VPN is detected, apps may send this data to authorities and also restrict user access internally.

Samokat and MegaMarket retrieve a **list of all installed VPN apps**, not just whether VPN is active.

Yandex Browser uniquely searches for **Tor** on the device.

No VPN detection found in 8 apps:
Yandex Market, Yandex Food, Mail.ru Mail, MegaFon, Mir Pay, Gosuslugi, Yandex Go, Zen.

---

### 2. Other surveillance behaviors

* **11 apps received a RED rating (maximum surveillance)**

* Banking apps are the most aggressive:

  * T-Bank, Sberbank, VTB rank in top 10
  * All send VPN status and use advanced fingerprinting and root detection
  * T-Bank requests 47 permissions (24 granted automatically)

* MegaMarket collects:

  * Contacts, SMS, call logs (via Group-IB SDK)

* Avito scans **200+ installed apps**

* Touch tracking (behavioral biometrics):

  * Apps record screen touches (coordinates, pressure, timing)
  * Includes T-Bank, Alfa-Bank, 2GIS, Yandex apps, Gosuslugi, Rutube, etc.

* Anti-analysis protection:

  * Apps detect tools like Frida
  * MAX obfuscates VPN interface names

* Major trackers:

  * AppMetrica (Yandex)
  * MyTracker (VK)
    → Present in over half the apps and accessible to law enforcement

---

## Recommendations

### For users in Russia

**Isolation**

* Ideally: two phones (one for Russian apps, one with VPN)
* Or use Android Work Profile (Shelter)

**VPN strategies**

* Use VPN at router level
* Split tunneling (partial protection)
* Fully stop apps before enabling VPN

**Permissions**

* Limit location, contacts, microphone, camera
* Revoke SMS and call log access

**Background activity**

* Restrict all apps from running in background

---

### For users outside Russia

**Isolation is critical**

* Russian apps can reveal your location via installed apps list

**Best setup**

* Separate device for Russian apps
* Or Work Profile

**Other steps**

* Disable location access
* Remove contacts access
* Use local SIM as primary
* Keep Russian SIM only for SMS (e.g., banking)

---

**Contact:** [info@rks.global](mailto:info@rks.global)
