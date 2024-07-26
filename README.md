# SQLMAP Automation Script

## Overview
This script automates various SQLMAP attacks using different tamper scripts. It is designed to work on both Arch and Debian-based systems and includes colorful output using `figlet`, `lolcat`, and `toilet`.

## Features
- Injection-based attacks
- File-based attacks
- Blind-based attacks
- Brute-based attacks
- Time-based attacks
- Error-based attacks
- Out-of-band attacks
- Database detection

## Prerequisites
- Arch-based systems: `pacman`
- Debian-based systems: `apt`
- Required tools: `sqlmap`, `figlet`, `toilet`, `lolcat`

## Installation
### For Arch-based Systems
```bash
sudo pacman -Sy --noconfirm
sudo pacman -S --noconfirm sqlmap figlet toilet lolcat
```

### For Debian-based Systems
```bash
sudo apt update -y
sudo apt install -y sqlmap figlet toilet lolcat
```

## Usage
```bash
./sqlmap_automation.sh <urls_file> <dbms>
```
- `<urls_file>`: File containing URLs to test.
- `<dbms>`: Database management system (e.g., MySQL, PostgreSQL).

## Example
```bash
./sqlmap_automation.sh urls.txt MySQL
```

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Disclaimer
This script is for educational purposes only. Use it responsibly and always seek permission before testing any systems. The author is not responsible for any misuse of this script.

## Author
Deepak aka FancybearIN

```

### Instructions for Adding to GitHub:

1. **Create a new repository** on GitHub.
2. **Clone the repository** to your local machine:
   ```bash
   git clone https://github.com/yourusername/your-repo-name.git
   ```
3. **Navigate to the repository directory**:
   ```bash
   cd your-repo-name
   ```
4. **Add the script and README file** to the repository:
   ```bash
   cp /path/to/your/sqlmap_automation.sh .
   cp /path/to/your/README.md .
   ```
5. **Commit the changes**:
   ```bash
   git add .
   git commit -m "Initial commit with script and README"
   ```
6. **Push the changes to GitHub**:
   ```bash
   git push origin main
   ```

This setup will ensure your script works on both Arch and Debian-based systems and includes a comprehensive README for GitHub. Let me know if you need any more adjustments!
