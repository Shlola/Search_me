# Search_me_v2
Searching things 
# Cat's search

A bash script that searches files for a word, sentence, or regex. It highlights
matches, decodes `.eml` email bodies (base64 and quoted-printable) so their text
is searchable, counts case variants, and can save timestamped reports.

## Features

- Search by plain word, sentence, or regular expression
- Built-in presets for IPv4, email, URL, MD5, SHA-1, SHA-256, and long Base64 strings
- Case-insensitive search, with a breakdown of each case variant found
- Optional whole-word matching and context lines around each match
- Decodes `.eml` files so text inside encoded email bodies can be found
- Colored output: filename in cyan, line number in gray, matches in pink
- Saves timestamped reports, and remembers past searches for the up arrow
- Skips `.git`, `node_modules`, `__pycache__`, and its own reports folder

## Requirements

- bash 4 or newer
- GNU grep and coreutils
- awk
- python3 (optional, only needed to decode `.eml` files)

Kali Linux includes everything above by default.

## Installation

```bash
git clone https://github.com/Shlola/Search_me_v2.git
cd cat-search
chmod +x Search_me.sh
```

## Usage

Interactive mode prompts for the pattern, the path, and the options:

```bash
./Search_me.sh
```

Quick mode runs one search with default options and does not save a report:

```bash
./Search_me.sh "password" /path/to/folder
./Search_me.sh "([0-9]{1,3}\.){3}[0-9]{1,3}" /var/log
```

Tab completes file and directory names at the path prompt. The up and down
arrows recall earlier patterns.

## Output and reports

Matches are printed with their filename, line number, and text. Case variants
are listed from most to least common. Reports are saved to:

```
~/findword_reports/report_YYYYMMDD_HHMMSS.txt
```

Search history is saved to `~/.findword_history`. Both files are readable only by you.

Reports and history can contain sensitive data, such as passwords or keys found
during a search. Delete them when you're done.

## Safety

- Terminal control characters are stripped from file contents before printing,
  so a malicious file can't change your terminal.
- Searches stop after 60 seconds, which guards against slow regex patterns.
- Symlinks named `.eml` are skipped, so their targets are not read.

## Project layout

```
cat-search/
├── Search_me.sh    # the script
├── README.md
└── .gitignore      # ignores reports, history, and .eml files
```

## Notes

- This script was written for searching your own files, such as your own
  email exports, logs, and notes. Only search data you have permission to read.
- The pink color needs a terminal with 256-color support.

## License

MIT (or choose another license before publishing).
