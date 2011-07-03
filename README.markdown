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

Full function reference is available at http://gopkgdoc.appspot.com/pkg/github.com/crazy2be/perms.