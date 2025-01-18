# Firmwalker

## Theory

Firmwalker is an automated tool designed to aid in the analysis of extracted Linux-based firmware file systems. It quickly identifies critical information such as password files, SSH keys, and configuration files, making it a useful tool for pentesters and security researchers focusing on embedded devices and IoT security.

#### Key Features

* Automated Scanning
  * Firmwalker parses through the entire extracted file system, looking for key files related to security, such as credentials, configuration files, and certificates.
* Focused Output
  * It categorizes findings such as passwords, SSH keys, web server information, and more, making it easy to focus on potential vulnerabilities.
* File System Search
  * Specifically designed for Linux-based firmware.
* Text File Parsing
  * Extracts useful information from plaintext configuration files and scripts.

## Cheat Sheet

```bash
# Clone the Firmwalker repository
git clone https://github.com/craigz28/firmwalker

# Navigate to the Firmwalker directory
cd firmwalker

# Run Firmwalker on an extracted firmware file system
./firmwalker /path/to/extracted/filesystem
```

## Installation

To use Firmwalker, you’ll need to clone the repository and run the script on a pre-extracted file system from a firmware image. Here’s how to get started:

1.  Clone the repository:

    ```bash
    git clone https://github.com/craigz28/firmwalker
    ```
2.  Navigate to the `firmwalker` directory:

    ```bash
    cd firmwalker
    ```
3. Ensure you have **bash** installed, as Firmwalker is a bash script.

## Usage

To run Firmwalker, the firmware image must first be extracted (you can use a tool like Binwalk for this). Once extracted, you can point Firmwalker to the root of the file system:

```bash
./firmwalker <path_to_extracted_firmware>
```

Firmwalker will then parse the file system and output a categorized report of its findings.

#### What Firmwalker Looks For

Firmwalker automatically searches for the following types of files and data in the extracted file system:

* Password Files: Looks for files such as `passwd`, `shadow`, and `login.defs`.
* SSH Keys: Searches for private keys (`id_rsa`), known hosts, and other SSH configuration files.
* Configuration Files: Identifies configuration files that may contain sensitive data, such as `config`, `.conf`, and `.ini` files.
* Web Server Info: Looks for web server files such as `nginx` or `httpd` configuration files, and web root directories.
* SSL Certificates: Finds SSL certificates and related private keys.
* Scripts: Parses through shell scripts or other automation scripts that might reveal hardcoded credentials or system configurations.
* Miscellaneous: Searches for any `.sql` files (databases), `crontab` files (schedules), and more.

## Example Command

Once the firmware has been extracted, run the following command to analyze the file system:

```bash
./firmwalker /path/to/extracted/filesystem
```

The output will be a structured list of findings, highlighting the critical files and directories of interest.

#### Example Output

Firmwalker provides a categorized output similar to:

```javascript
--- Password Files ---
/etc/passwd
/etc/shadow

--- SSH Keys ---
/root/.ssh/id_rsa

--- Configuration Files ---
/etc/nginx/nginx.conf
```

#### Additional Notes

* Firmwalker works on an extracted file system, meaning you’ll need to extract the firmware first before running the tool.
* The findings give a quick overview of critical files to investigate further, making it ideal for initial reconnaissance of firmware images.

## Resources

* [Firewalker Git repository](https://github.com/craigz28/firmwalker)
