> [!NOTE]
> RKS Global has translated the article.
> You can read the official translation here: https://rks.global/en/research/vpn-detection/

# About this repo

This is automated translation of article from RKS Global. Please visit their website and feel free to share both links.

Link to the original article in Russian: https://rks.global/ru/research/vpn-detection

Link to this translation: https://github.com/mitsuha44/how-and-why-russian-apps-search-for-vpns-on-users-phones/blob/main/README.md

# Full article bellow

---

## RKS Global

**April 2026**

# How and Why Russian Apps Search for VPNs on Users’ Phones

**An analysis of surveillance in 30 popular Russian Android apps**

## Context

Russian authorities intend to require major domestic digital companies to participate in censorship and user surveillance. This became known in early April 2026, when the Ministry of Digital Development, Communications and Mass Media of the Russian Federation held special meetings with the largest Russian internet companies by audience size: Sber, Yandex, VK, Wildberries, Ozon, Avito, X5, and others — more than 20 platforms in total.

According to available information, companies were instructed to restrict access to internet services for users whose devices have VPN enabled by April 15, 2026. Those who fail to comply may face the [loss of IT accreditation](https://www.kommersant.ru/doc/8552209), benefits, removal from the “whitelist,” and effectively the inability to operate under restricted internet conditions.

Guidelines sent by the Ministry [describe](https://t.me/ru_tech_talk/1048) stages of checks that apps must perform on user devices. Apps are expected to scan network settings, routing and DNS, detect system-level VPNs and proxies, and analyze user behavior — such as sudden country changes or unusual connection patterns.

Experts believe this level of data collection increasingly resembles spyware [disguised](https://t.me/amnezia_vpn_news_ru/99) as useful services, as it involves access to sensitive technical device information that can be used not only to detect configurations but also to deanonymize users. This data is expected to be shared with Roskomnadzor to help identify VPN services that have not yet been blocked.

Authorities are also requiring companies not only to monitor users but to penalize those using VPNs — degrading service quality or restricting access to push users away from circumvention tools. This effectively delegates censorship from the state to private companies, forcing them to bear development costs, legal risks, false positives, and customer loss.

As early as April 7, 2026, users in Russia [reported](https://t.me/paperpaper_ru/67292) issues accessing Wildberries, Ozon, and VkusVill while using VPNs: slow loading, unavailable product pages, or full service disruption. Previously, services only warned about “incorrect operation with VPN,” but now actively [restrict](https://iz.ru/2073656/anton-belyi/marketplejsy-nachali-borbu-s-programmami-dlya-obhoda-blokirovok%29) access.

*Digital censorship in Russia is reaching a new level. Experts note a shift from passive internet censorship to active measures. Since 2012, most blocks and sanctions have been carried out by censors. Initially, they manually compiled a registry of banned websites and passed it to providers to enforce blocking. Later, they deployed the TSPU system to automatically detect and restrict suspicious or undesirable traffic. At the new stage — which is taking shape right now — additional data is being collected directly from users’ devices, and decisions about blocking are made based on this information.*

## Hypothesis

RKS Global previously [studied](https://www.techradar.com/vpn/vpn-privacy-security/russias-state-backed-max-app-may-know-if-you-are-using-a-vpn-to-bypass-censorship-here-is-everything-we-know) how the MAX messenger detects active VPN connections on Android and sends this data to developers cooperating with Russian law enforcement. VPN providers have already experienced server IP blocking linked to such reports.

Given government pressure and early success, experts hypothesize that many Russian apps will begin detecting VPN usage and reporting it to regulators. This method is highly effective and likely to expand.

> The hypothesis: not only MAX, but potentially any Russian Android app may monitor devices for VPN usage, with deep system access and extensive data collection — possibly exceeding official requirements.

## Methodology

Experts analyzed 30 of the most popular Russian Android apps to determine what VPN-related data they collect and the extent of surveillance.

Selection was based on MAU (Monthly Active Users), using data from Mediascope (Dec 2025–Feb 2026), RuStore download rankings, company reports (Sber, VK, Ozon, 2GIS), and media publications.

Static APK analysis was used — decompilation via apktool and jadx, with searches across 68 tracking checkpoints in 12 tracking categories. APK versions were obtained from RuStore and Google Play and are current as of April 2026.

Methodology limitations. Only static analysis was conducted, without dynamic testing on a device.

## Findings

### 1. Apps That Monitor VPN Usage

**The analysis found that 22 out of 30 apps detect VPN usage, and 19 of them send VPN status to their servers.**

These apps include: Yandex Browser, Yandex Maps, VKontakte, My MTS, Sberbank Online, T-Bank, VK Video, Wildberries, Kinopoisk, Ozon, Samokat, RuStore, VTB Online, Yandex Music, Avito, Alfa-Bank, 2GIS, MegaMarket, Odnoklassniki, MAX, Rutube, VK Music.

When an app detects a VPN, it may send this information to censors, enabling more effective blocking measures. Additionally, the company behind the app may independently penalize the user by restricting or significantly complicating access to its services.

Detecting a VPN means identifying that a user is hiding their real IP address. This information can be (and is) transmitted to company servers, from where it may become accessible to law enforcement agencies.

At the time of the study, no evidence of VPN detection was found in 8 of the 30 analyzed apps: Yandex Market, Yandex Food, Mail.ru Mail, MegaFon, Mir Pay, Gosuslugi, Yandex Go, Zen.

The apps Samokat and MegaMarket retrieve a list of all VPN apps installed on the device (using queryIntentServices("android.net.VpnService")). This means they don’t just check whether a VPN is active—they identify which specific VPN apps are installed.

Yandex Browser is the only app found to search for Tor on the device. In other words, a browser that itself offers an “Incognito” mode is also looking for anonymity tools on the user’s device. Overall, Yandex Browser and Yandex Maps use the highest number of VPN detection methods (4 out of 6).

### 2. Apps That Track Users in Other Ways

According to the analysis, 11 out of 30 apps received a RED rating (maximum tracking intensity, see the table in the appendix).

Banking apps are the most aggressive group. T-Bank (65), Sberbank (64), and VTB (59) are in the top 10. All three send VPN status to servers, use advanced device fingerprinting, detect root access, and employ analysis tools. T-Bank requests 47 permissions — the highest number overall. Of these, 24 (including autostart, background camera and microphone services, location access, and APK installation) are granted automatically without user awareness. Banking apps lead in the number of “silent” install-time permissions (a standard term in Android development; official Google documentation defines install-time permissions as those granted automatically upon installation, such as INTERNET or BLUETOOTH, as opposed to runtime permissions requested during app use), forming a persistent background infrastructure.

The MegaMarket app (owned by Sber) is tied for first place with T-Bank. It uses the Group-IB SDK and collects contacts, SMS, and call logs.

The Avito app scans more than 200 third-party apps. In its Android manifest `<queries>` block, over 200 packages are listed — banks (Sberbank, T-Bank, VTB, Alfa), marketplaces (Ozon, Wildberries), social networks (VK, Telegram, Instagram, Facebook), services (Yandex), and competitors (Drom, CIAN, HH.ru). Avito can determine which of these apps are installed on the device.

Apps such as T-Bank, Alfa-Bank, 2GIS, Yandex Food, MegaMarket, My MTS, Odnoklassniki, Gosuslugi, Rutube, Sberbank Online, and Yandex Music intercept every screen touch event with coordinates, pressure, and timing (`dispatchTouchEvent`). Sberbank stores TouchData objects with fields like pressure, size, x, and y. The Group-IB SDK (used in Alfa-Bank, MegaMarket, and My MTS) intercepts all touch events. This behavioral biometrics approach allows identifying users based on how they interact with the screen—even without login. Rutube records touch coordinates despite being a simple video platform.

Apps like T-Bank, Yandex Browser, Yandex Music, and Yandex Maps search for traces of Frida (a dynamic analysis tool), meaning they actively try to prevent users or researchers from analyzing their behavior. Yandex Music protects itself in a way comparable to military-grade software.

MAX obfuscates network interface names (tun/ppp/tap/pptp0 encoded as byte arrays), indicating intentional concealment of VPN detection mechanisms from researchers.

AppMetrica (Yandex) and MyTracker (VK) are the two main Russian tracking SDKs, embedded in more than half of the analyzed apps. Data from these SDKs may be accessible upon request by Russian law enforcement agencies.


## Recommendations

### Part 1. For users in Russia

1.1 **Isolation**

- The ideal option is to have two phones. One for Russian apps, and the other for everything else using a VPN.

- If you only have one phone, you should use an Android Work Profile via [Shelter](https://f-droid.org/packages/net.typeblog.shelter/). With this setup, apps from different profiles cannot see each other: not the list of apps, contacts, or files. The Work Profile does not hide the VPN—only the data between profiles—so it does not help protect VPN applications.

1.2 **VPN**

- **VPN on the router**. A VPN tunnel is created on the router, and the phone connects via Wi-Fi.

- **Split tunneling** (a partial solution). Some VPN clients allow you to exclude Russian apps from the tunnel. Their traffic goes directly, without passing through the VPN. This helps against some checks, but apps that scan tun0 will still detect the VPN.

- **Disabling apps on the device**. It’s recommended to turn off spying apps before using a VPN. It’s important to actually stop them, not just minimize them, since apps can run in the background and may detect the moment the VPN is activated.

1.3 **Revoke Unnecessary Permissions**

- Location access should be left only for navigation apps, and only set to “while in use.”

- Access to contacts should be revoked for all apps except messengers.

- Access to the microphone and camera should be allowed only upon request.

- Access to call logs and SMS should be revoked for all apps.

1.4 **Background Activity**

All 30 analyzed apps start automatically and run in the background. They should be restricted: Settings → Apps → Battery → “Restricted.” Do not allow them to bypass battery optimization.

### Part 2. For users outside Russia

2.1 **Isolation Is Mandatory**

If foreign apps are installed on the same phone alongside Sberbank apps, any of those apps that send the list of installed programs to a server can reveal your country.

- **The best option is to use two phones**. It’s worth dedicating an old iPhone exclusively to Russian apps.

- **If you only have one phone**, you must use a Work Profile via [Shelter](https://f-droid.org/packages/net.typeblog.shelter/). This way, Russian apps won’t be able to see the list of apps in the main profile.

2.2 **Location**

Location permissions should be revoked for all Russian apps. Navigation abroad should be done only through Google Maps and similar services.

2.3 **Contacts**

It’s better to revoke access to contacts for all Russian apps. While abroad, your contacts will include local people and organizations.

2.4 **SIM Card**

A Russian mobile operator can detect roaming when a user connects to its SIM card abroad. It should be set to “SMS only” mode (for example, for banking verification codes). Ideally, the Russian SIM is used in a phone dedicated to Russian apps, while the main (local foreign) SIM is used in your primary phone.

**Contact:** [info@rks.global](mailto:info@rks.global)

---
