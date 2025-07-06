- Top level security/administrative boundary in AD environments.
- Contains one or more domains sharing common schema, config and global catalog.

![[Forests.png]]
# Characteristics

- Forest root domain is the first created and remains central.
- All domains in a forest:
	- share the same schema.
	- share a config partition.
	- can trust each other (automatic transitive trusts).
- A forest can contain:
	- multiple trees.
	- multiple domains.
	- one or more domain controllers per domain.
- Admins from one forest cannot control another unless explicitly trusted.
# Trust Relationships

- Forests can be linked via:
	- forest trusts (one-way/two-way)
# Notes

- Forests functional level defines which AD features are available.
- Each forest has:
	- one schema master.
	- one domain naming master.
	- one or more global catalog servers.

