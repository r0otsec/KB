- Built-in credential storage system
- Saves/manages usernames, passwords and certificates.
- Found under:
	- `Control Panel` -> `User Accounts` -> `Credential Manager`

![[Cred Manager.png]]
# Types

- `Windows Credentials`:
	- Network shares, RDP, file shares
	- Domain-based credentials
- `Web Credentials`:
	- Internet Explorer and Edge browser passwords.
- `Generic Credentials`:
	- App-specific (Outlook, OneDrive, Teams)
	- Stored by third-party apps using Windows APIs
# Storage

- Stored in encrypted format via [[DPAPI]].
- File locations (per user):
	- `C:\Users\<user>\AppData\Roaming\Microsoft\Credentials\`
	- `C:\Users\<user>\AppData\Local\Microsoft\Credentials\`
- Decryption tied to:
	- user logon creds.
	- domain recovery keys (if in AD).
# Notes

- Often overlooked source of cleartext credentials.
- No user prompt when applications silently save to it.
- Cleared manually or via:
	- `cmdkey /delete:<target>`

