<h1 align="center">
HIBPv7 Hash Cracking Resources
</h1>

> [Update 10/15/2023] - Temporarily unarchived the repository to update references. Some of the projects used are now legacy with other solutions taking their place. This repository will be maintained as a historical reference point for HIBPv7.

I needed a large sample of actual password hashes for analysis to improve password security. The HaveIBeenPwned repository was a great collection of password hashes from breaches and covered a diversity of environments. The hashes were made public and over time I cracked them for analysis:

- `HIBPv7`: 578,006,177/613,584,246 (94.20%) passwords

Resources in this repository use this sample as a base of real-world passwords and are utilized in a few different applications.

While looking at the HIBP dataset, I realized that many passwords were low quality and would not meet AD password complexity requirements. I wanted to clean up the input data because the better the input set, the better the output. I created filtered sub lists to provide meaningful analysis that could be used to develop other resources.

## Getting Started:
 - [Wordlists](#wordlists)
 - [Masks and Tokens](#masks-and-tokens)
 - [Summary](#summary)

## Wordlists
**HIBPv7_7M.txt**: Contains the top 7 million most popular passwords from HIBPv7 in no particular order. From the top 7 million most popular passwords, I cracked 99.65% of them, and this is the resulting list.

**HIBPv7_100M-min-reqs.txt**: From the top 100 million most popular passwords in HIBPv7, I cracked 99.18% of them, and this is the result after filtering for minimum complexity requirements. The wordlist contains around 8.5 million passwords.

**HIBPv7_Top15_Masks-min-reqs.txt**: Wordlist from the filtered down HIBP data (~70m passwords) and the set's top 15 most popular password masks. The wordlist contains around 30 million passwords and would meet the minimum complexity requirements of most password policies.

## Masks and Tokens
**Password Masks**: These password masks are in `Hashcat` format taken from the filtered down HIBP dataset and sorted by most popular.

**Common tokens**: A list of password tokens is generated using the Python NTLK library. The passwords were passed to a parser that attempted to filter down the passwords to their base tokens and then sorted by most common. This list results from parsing tokens from the filtered down HIBP set.

## Summary:
- Wordlists:
    - `HIBPv7_7m.txt`
        - Top 7M passwords (99.65%) from HIBPv7
    - `HIBPv7_100M_min-reqs.txt`
        - 8.5m passwords from HIBPv7 that would meet min AD complexity requirements
    - `HIBPv7_Top15_Masks-min-reqs.txt`
        - 30m passwords from HIBPv7 based on the top 15 masks that would meet min AD complexity requirements
- Masks and Tokens
    - `password_masks_min-reqs`
        - Most popular password masks from all HIBP data filtered for minimum complexity requirements.
    - `password_masks_no-reqs`
        - Most popular password masks from all HIBP data filtered for passwords greater than or equal to 8 characters.
    - `common_tokens_min-reqs`
        - Most popular password words/tokens from all HIBP data filtered for minimum complexity requirements.
    - *Text files are just the words and csv files contain additional metadata*

