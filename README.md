# YubiKey SSH Key Generator and Bitwarden Storage

This Python script automates the process of generating a YubiKey-based SSH key and storing it securely in Bitwarden using rbw, an unofficial command-line client for Bitwarden. It simplifies the setup of FIDO2 security keys for SSH authentication while ensuring the keys are backed up in a password manager.

## Features

- Generates an ED25519-SK SSH key using a YubiKey
- Optionally creates a key without touch requirement
- Optionally creates a key requiring user verification (e.g., PIN entry)
- Retrieves YubiKey information (serial number or device type)
- Creates a Bitwarden entry with the generated SSH key and YubiKey information using rbw

## Prerequisites

- Python 3.x
- YubiKey Manager (ykman)
- OpenSSH with FIDO2 support
- rbw (Unofficial Bitwarden CLI: https://github.com/doy/rbw)

## Installation

1. Clone this repository or download the script.
2. Ensure you have the required dependencies installed.
3. Install rbw following the instructions on its GitHub page: https://github.com/doy/rbw

## Options

- `--no-touch-required`: Generate an SSH key that doesn't require physical touch for authentication (less secure)
- `--verified-required`: Generate an SSH key that requires user verification (e.g., PIN entry) for authentication

## Usage

Run the script with Python:

./yubikey_ssh_bitwarden [options]


Examples:
`./yubikey_ssh_bitwarden`  
`./yubikey_ssh_bitwarden --no-touch-required`  
`./yubikey_ssh_bitwarden --verified-required`  


## How It Works

1. Unlocks Bitwarden vault using rbw
2. Prompts for a name for the new SSH key
3. Generates an ED25519-SK SSH key using the YubiKey
4. Retrieves YubiKey information (serial number or device type)
5. Creates a Bitwarden entry using rbw, containing the private key, public key, and YubiKey information

## Security Considerations

- The script stores an encrypted version of the SSH private key in Bitwarden. The key cannot be used without the YubiKey that it was created with. Ensure your Bitwarden account is properly secured.
- Using the `--no-touch-required` option reduces security by not requiring physical touch for authentication.
- Using the `--verified-required` option enhances security by requiring user verification (e.g., PIN entry) for authentication.
- rbw maintains a background process to hold keys in memory, similar to ssh-agent or gpg-agent. This improves usability but requires proper system security.

## About rbw

rbw is an unofficial command-line client for Bitwarden that offers improved usability over the official CLI. It maintains a background process to hold keys in memory, allowing for simpler interaction without manually managing lock/unlock states or environment variables.

For more information about rbw, including installation instructions for various platforms, configuration options, and usage details, visit the [rbw GitHub repository](https://github.com/doy/rbw).

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is open source and available under the MIT License.
