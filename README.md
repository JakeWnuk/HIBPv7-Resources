<h1 align="center">
Hash Cracking Resources
</h1>

## What is this?
This repository aims to aggregate several custom hash cracking resources into a single location for reference and help guide using these resources to secure environments.

## What is in this?
I needed a large sample of actual password hashes for analysis to improve password security. The HaveIBeenPwned repository was a great collection of password hashes from actual breaches and covered a great diversity of environments. The hashes were made public and contained 613,584,246 passwords (v7), and over some time, I cracked 578,006,177 (94.20%) of them for analysis. Resources in this repository use this sample as a base of real-world passwords and are utilized in a few different applications.

While looking at the HIBP dataset, I realized that many passwords were pretty bad, junky, and would not meet AD password complexity requirements. Because I primarily used this resource for internal assessments, I wanted to clean up the input data because the better the input set, the better the output. I created [PwdStat](https://github.com/JakeWnuk/PwdStat) to filter down password lists and provide meaningful analysis that could then be used to develop other resources.

## Wordlists
**HIBP-Top-7M.txt**: this wordlist contains the top 7 million most popular passwords from HIBP in no particular order. From the top 7 million most popular passwords, I cracked 99.65% of them, and this is the resulting list.

**HIBP-Top-100M-minreqs.txt**: this wordlist contains the top 100 million most popular passwords from HIBP in no particular order. From the top 100 million most popular passwords, I cracked 99.18% of them, and this is the result after filtering for minimum complexity requirements. The wordlist contains around 8.5 million passwords.

**Top15_masks_passwords.txt**: I created this wordlist from the filtered down HIBP data (~70m passwords) and the set's top 15 most popular password masks. The wordlist contains around 30 million passwords (>2x the size of RockYou) and would meet the minimum complexity requirements of an AD domain.

## Masks and Tokens
**Common masks**: These password masks are in `Hashcat` format taken from the filtered down HIBP dataset and sorted by most popular. These masks can be greatly helpful in masks attacks as they are the most likely masks from real users' passwords. Additionally, the `_w_count` set provides additional metadata about the generated masks that offensive practitioners can filter against for specific applications.

**Common tokens**: Using [PwdStat](https://github.com/JakeWnuk/PwdStat), a list of password tokens is generated using the NTLK library. The passwords were passed to a parser that attempted to filter down the passwords to their base tokens and then sorted by most common/popular. This list results from parsing tokens from the filtered down HIBP set. It can be valuable for reducing keyspace in mask attacks or PRINCE attacks as a list of tokens to create new password combinations. 

## Rules
The repository contains various rules generated from the unfiltered and filtered HIBP set using unique methods. They are separated into smaller lists to account for different hashing algorithms and sorted by most effective (most cracks) to least effective.
A methodology writeup can be found [here for Squid Rules](https://jakewnuk.com/posts/cracking-half-billion-passwords-custom-rules-wordlists/) and [here for Leo Rules](https://jakewnuk.com/posts/cracking-half-billion-passwords-analysis/).

**Squid Rules**: This ruleset was created using rounds of randomized hashes, wordlists, and rule order to sort Hashcat rules by effectiveness. The set was "trained" on the entire collection of HIBP passwords and only included rules found in public hash cracking rule sets. The set is sorted by most effective to least effective and does not contain any generated rules. 

**Leo Rules**: This ruleset was created using rounds of randomized hashes, wordlists, and rule order to sort Hashcat rules by effectiveness. The set was "trained" on the filtered collection of HIBP passwords and only included generated rules (raking) not found in public hash cracking rule sets. The set is sorted by most effective to least effective and contains generated rules. I performed around 3000 rounds of raking to achieve this optimized set. 
