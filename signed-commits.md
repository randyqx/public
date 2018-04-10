# Signed git commits

This is a hack from srs on how to enforce a policy that commits to a
git repository are pgp signed by the committer.  The purpose is to
provide attribution of all changes and, one hopes, thereby deter
malicious commits.

One signs commits to a repo using

   ```git commit -S <foux>```

which is enforced by having

```
  [commit]
      gpgsign = true
```

in your `<repo>/.git/config`

and by having `<repo>/.git/hooks/pre-push`

    #!/bin/sh

    # An hook script to verify what is about to be pushed is signed.  Called by "git
    # push" after it has checked the remote status, but before anything has been
    # pushed.  If this script exits with a non-zero status nothing will be pushed.
    #
    # This hook is called with the following parameters:
    #
    # $1 -- Name of the remote to which the push is being done
    # $2 -- URL to which the push is being done
    #
    # If pushing without using a named remote those arguments will be equal.
    #
    # Information about the commits which are being pushed is supplied as lines to
    # the standard input in the form:
    #
    #   <local ref> <local sha1> <remote ref> <remote sha1>
    #
    # This script uses "git verify-commit" to check whether all of the commits
    # being pushed have been signed by known keys (most likely your own, but
    # the script doesn't check that).

    remote="$1"
    url="$2"

    z40=0000000000000000000000000000000000000000

    while read local_ref local_sha remote_ref remote_sha
    do
	    if [ "$local_sha" = $z40 ]
	    then
		    # Handle delete
		    :
	    else
		    if [ "$remote_sha" = $z40 ]
		    then
			    # New branch, examine all commits
			    range="$local_sha"
		    else
			    # Update to existing branch, examine new commits
			    range="$remote_sha..$local_sha"
		    fi

		    if ! git verify-commit `git rev-list "$range`
		    then
			    echo >&2 "Could not verify commit signatures, not pushing"
			    exit 1
		    fi
	    fi
    done

    exit 0

---

2018.04.10
