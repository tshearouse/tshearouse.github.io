
# Github tips and tricks

# Codeowners

Add a codeowners file to make github auto-tag reviewers on PR's
 - Follows same syntax as a .gitignore file, roughly
 - Pattern whitespace @username
	 - Any whitespace will work
	 - '#' denotes a comment
	 - The last match wins. Put blankets like `* @admin` on top, and specific stuff like `/logs/**.conf @wat` at the end
 - Literally name the file `CODEOWNERS` with no extension. Put it at the root of your repo.

## Why doesn't codeowners work?

Because there are a bunch of subtle rules that aren't well documented, and breaking any of these rules will cause your codeowners file to silently fail. 
 - While I'm pretty sure anyone can edit the codeowners file, an admin needs to enable it. It's in the branch protection settings alongside the "require PR reviews" settings
 - Every user or group referenced in the codeowners file must have push access to the repository
 - It's touchy about special characters. I don't know the full list, but patterns cannot contain `&` or `,` 
 - Remember that `/path/*` will only match files inside the `/path` directory. Use `/path/**` if you want a recursive match  

# PR's and Issues

There's a lot of cool integration inside github. Numeric id's are unique inside a repository - a PR number and an issue number can never be the same. This means you can:
 -  Close an issue with a pull request. Include the text `resolves #123` in a pull request description, and issue #123 will automatically close when that pull request is merged.
 - Reference another pull request or issue just by entering `#123` in a comment, description, or commit message. 
	 - Weird implication: This means you should use markdown for numbered lists. If you have `#1`, `#2`, etc in a comment, these will be automatically (and possibly incorrectly) associated with a PR or issue. World, please stop doing this. It's confusing to see an auto-attribution on an issue claiming that it was referenced in an unrelated conversation.
