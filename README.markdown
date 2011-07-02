HTTP Permissions Management Library
===================================

**In progress, Incomplete!**
A simple authentication module that supports user and group based authentication methods, with users authenticated via e-mail addresses.
In order to use it, you pass a http.Request to the Get() function, which returns the permissions of the current user based on the most permissive interpretation of their permissions and the permissions of their group.
Uses the session library (http://github.com/crazy2be/session) key "openid-email" to get the name of the user we are currently serving.

Getting Started
---------------

Install:

	goinstall github.com/crazy2be/perms

Import:

	import "github.com/crazy2be/perms"

Use:

	p, err := perms.Get(r)

	if !perms.Read {
		template.Error403(c, r, "Access Denied!")
	}


Functions
---------

	type Permissions struct {
			Read  bool
			Write bool
			// Is the user authenticated at all? Aka 1) do they have a session cookie, and 2) have they logged in?
			Authenticated bool
			// Is the user recognized by the system? Do they have an account?
			Recognized bool
			// What path are these permissions for?
			Path string
	}

TODO: Do we want more permissions here?

## func Get(r *http.Request) (p *Permissions, err os.Error)
Basic function that retrieves the permissions a user has based on the contents of their request, including cookies and request path. Designed to be a simple function for most uses. If you want more control, you can use the GetGroupPerms and GetUserPerms functions.

### func GetGroupPerms(name, path string) (p *Permissions, err os.Error)
Retrieves the permissions for all members of a group with the given name.

### func GetUserPerms(name, path string) (p *Permissions, err os.Error)
Retrieves the user permissions, and the user permissions ONLY, for a user with a given name. Does not take group membership into account, and is likely not that useful for this reason.