<h1 align="center">
Password Security Repository
</h1>

## What is this?
I wanted to take some time to research password security and hash cracking from an offensive perspective. Along the way, I learned several new techniques and built new tools to help security practitioners help improve their password security. This repository aims to aggregate several resources into a single location for reference and help guide how to best use these resources to secure environments. 

## What is in this?
I needed a large sample of actual password hashes for analysis to improve password security. The HaveIBeenPwned repository was a great collection of password hashes from actual breaches and covered a great diversity of environments. The hashes were made public and contained 613,584,246 passwords, and over several months I cracked 578,006,177 (94.20%) of them for analysis. Many of the resources in this repository use this hash sample as a base of real-world passwords and have been utilized in a few different applications for tooling.

While I was looking at the HIBP dataset, I realized that many passwords were pretty bad, junky, and would not meet an internal AD environment password complexity requirement. Because I primarily used this resource for internal assessments, I wanted to clean up the input data because the better the input set, the better the output. I created [PwdStat](https://github.com/JakeWnuk/PwdStat) to filter down password lists and provide meaningful analysis that could then be used to develop other resources. 

## Wordlists
**HIBP-Top-7M.txt**: this wordlist contains the top 7 million most popular passwords from HIBP de-duplicated and in no particular order. From the top 7 million most popular passwords, I cracked 99.65% of them, and this is the resulting list. Offensive practitioners can use this wordlist for hash cracking, and defenders may find this list valuable to deny users from setting passwords contained in this list to improve security. 

**Top15_masks_passwords.txt**: I created this wordlist from the filtered down HIBP data (~70m passwords) and the top 15 most popular password masks of the set. The wordlist contains around 30 million passwords (>2x the size of RockYou) and would meet the minimum complexity requirements of an AD domain. 

## Masks and Tokens
**Common masks**: These password masks are in `Hashcat` format taken from the filtered down HIBP dataset and sorted by most popular. These masks can be greatly helpful in masks attacks as they are the most likely masks from real users' passwords. Additionally, the `_w_count` set provides additional metadata about the generated masks that offensive practitioners can filter against for specific applications.

**Common tokens**: Using [PwdStat](https://github.com/JakeWnuk/PwdStat), a list of password tokens is generated using the NTLK library. The passwords were passed to a parser that attempted to filter down the passwords to their base tokens and then sorted by most common/popular. This list results from parsing tokens from the filtered down HIBP set. It can be valuable for reducing keyspace in mask attacks by limiting the special characters or PRINCE attacks as a list of tokens to create new password combinations. 

## Rules
The repository contains various rules generated from both the unfiltered and filtered HIBP set using unique methods. They are separated into smaller lists to account for different hashing algorithms and sorted by most effective (most cracks) to least effective. *A methodology writeup is comming soon (tm).*

**Squid Rules**: This ruleset was created using rounds of randomized hashes, wordlists, and rule order in a high entropy environment to sort Hashcat rules by effectiveness. The set was "trained" on the entire collection of HIBP passwords and only included rules found in public hash cracking rule sets. The set is sorted by most effective to least effective and does not contain any generated rules. 

**Leo Rules**: This ruleset was created using rounds of randomized hashes, wordlists, and rule order in a high entropy environment to sort Hashcat rules by effectiveness. The set was "trained" on the filtered collection of HIBP passwords and only included generated rules not found in public hash cracking rule sets. The set is sorted by most effective to least effective and contains generated rules. The filtered collection of HIBP was very difficult for most rule sets to crack, making it a good candidate for rule raking. I performed around 3000 rounds of raking to achieve this optimized set. 