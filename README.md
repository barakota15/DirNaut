# DirNaut - Powerful Directory & URL Enumeration Tool

![Bash Script](https://img.shields.io/badge/bash-script-blue) [![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

DirNaut is a Bash-based enumeration tool that discovers directories, URLs and web resources across domains using multiple auxiliary tools and techniques, with optional probing of found URLs.

<img width="1115" height="628" alt="image" src="https://github.com/user-attachments/assets/ae01a021-ea11-4d92-8350-802fd88994fc" />

---

## Table of Contents

1. [Features](#features)  
2. [Requirements](#requirements)  
3. [Installation](#installation)  
4. [Usage](#usage)  
5. [Examples](#examples)  
6. [Contributing](#contributing)  
7. [License](#license)  
8. [Author](#author)  

---

## Features

- Integrates many enumeration and scraping tools:
  - `ffuf` for fuzzing directories
  - `gau` for gathering URLs
  - `dirsearch` (GET / POST / advanced modes)
  - `waybackurls` for historical URLs
  - `katana` spidering
  - `gospider`
  - `paramspider`
  - VirusTotal domain-based URL collection
- Accepts a single domain or a file with multiple domains
- Ability to include or exclude specific tools using flags
- Extract specific file types (JavaScript, PHP, web files) or URLs with parameters
- Deduplicates and merges results
- Optionally probes discovered URLs via `httpx` to filter by HTTP status codes
- Supports silent mode, color disabling, debug mode
- Customizable output file names

---

## Requirements

Ensure the following tools/commands are installed and accessible in your PATH:

- `ffuf`  
- `gau`  
- `dirsearch`  
- `waybackurls`  
- `katana`  
- `gospider`  
- `paramspider`  
- `httpx`  
- `jq`  
- `curl`  

---

## Installation

1. Install the required tools (see Requirements).  
2. Clone or copy the repository containing DirNaut:  
   ```bash
   git clone https://github.com/barakota15/DirNaut.git
   cd DirNaut
   ```
3. Make the script executable:

   ```bash
   chmod +x dirnaut.sh
   ```
4. (Optional) Add to PATH for easy usage:

   ```bash
   sudo ln -s $(pwd)/dirnaut.sh /usr/local/bin/dirnaut
   ```

---

## Usage

```bash
./dirnaut.sh [flags]
```

### Input Flags:

* `-d, --domain <domain>` : Target domain for enumeration
* `-D, --domains <file>` : File containing multiple domains
* `--ffuf <file>` : Wordlist file for `ffuf` directory fuzzing (default: `./wordlist/directories.txt`)
* `--api <API key>` : VirusTotal API key (optional)

### Filtering / Tool Selection Flags:

* `-t, --tools [tool1,tool2,...]` : Use only specific tools (default: all)
* `-f, --filter [tool1,tool2,...]` : Exclude specific tools from execution

### Extraction Flags:

* `-ej, --extract-javascript` : Extract `.js` files from discovered URLs
* `-ep, --extract-php` : Extract `.php` files
* `-ew, --extract-web-files` : Extract web‑related files (html, asp, xml, etc.)
* `-p, --extract-parameters` : Extract URLs containing query parameters and sensitive tokens

### Output / Probing Flags:

* `-o, --output <file>` : Name of final output file (default: `all_urls.txt`)
* `--no-httpx` : Skip probing URLs with `httpx`
* By default, `httpx` probes discovered URLs for HTTP status codes 200, 301, 302, and 403

### Debug / Help / Miscellaneous Flags:

* `-h, --help` : Display usage help and exit
* `-v, --version` : Print version information
* `-ls, --list-sources` : List all supported enumeration sources/tools
* `-s, --silent` : Silent mode (minimal log output, only result URLs)
* `-nc, --no-color` : Disable colored output
* `--debug-mode` : Enable verbose/debug logs

---

## Examples

* Run enumeration on a single domain using default tools and HTTP probing:

  ```bash
  ./dirnaut.sh -d example.com
  ```

* Use a domains file, filter out `katana` and `paramspider`, and output to `urls.txt`:

  ```bash
  ./dirnaut.sh -D domains.txt -f katana,paramspider -o urls.txt
  ```

* Enumerate with JavaScript and PHP extraction, skip HTTP probing:

  ```bash
  ./dirnaut.sh -d example.com -ej -ep --no-httpx
  ```

* Run in silent mode (just URLs):

  ```bash
  ./dirnaut.sh -d example.com -s
  ```

---

## Contributing

Contributions are welcome! You can:

* Report issues or suggest enhancements
* Submit pull requests with fixes, new features, documentation improvements

Please follow the existing coding and formatting style.

---

## License

This project is licensed under the [MIT License](https://github.com/barakota15/DirNaut?tab=MIT-1-ov-file). See the `LICENSE` file for details.

---

## Author

**DirNaut** by *Barakota15* — version 1.1
