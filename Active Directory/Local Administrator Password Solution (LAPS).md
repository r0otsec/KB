- Automatically manages and randomizes local Administrator password on domain systems.
# How It Works

- Each computer stores its local admin password in secure AD attribute.
- Password is:
	- randomized on a schedule
	- stored in plaintext in AD
	- protected using [[ACL (Access Control List)|ACLs]] on computer object
- AD schema extension adds:
	- `ms-Mcs-AdmPwd` - stores password.
	- `ms-Mcs-AdmPwdExpirationTime` - tracks expiration.
# Detection/Auditing

- Tips for auditing:
	- track who has `ReadProperty` rights on `ms-Mcs-AdmPwd`
	- use BloodHound to find over-permissioned groups.
- Monitor for:
	- excessive LAPS password reads.
	- password reads by non-IT personnel.
# Notes

- To use it, you must extend the AD schema (adding new attributes to AD object types).
- For more recent versions (Windows 10/11/Server 2022+), attributes change:
	- `msLAPS-Password`
	- `msLAPS-PasswordExpirationTime`
	- `msLAPS-EncryptedPassword`

