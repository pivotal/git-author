# git-author
A simple tool to add multiple authors to commit mesages. Under the hood it is
based on `git commit --template` and depends on `git-together`.

# Setup
1. Follow the instructions from https://github.com/kejadlen/git-together to set up
   the `git-together` configurations.
2. Run `setup.sh`.
3. Add `export GIT_TOGETHER_NO_SIGNOFF=1` to your environment (e.g. in
   `~/.bashrc` on Linux or `~/.bash_profile` on MacOS). This will disable the
   `--signoff`s added by `git-together commit`.

# Usage
Set the authors as below:
```
# pairing with James and Naomi
git author jh nn

# soloing
git author jh

# mobbing
git author jh nn ca

# show who are included in current ~/.git-author
git author
```

After doing so, `git commit` will now automatically include all of the authors
in the commit message with the prefix `Co-authored-by:` or `Authored-by` if there
is only one author. For example:

```
# mobbing
git author jh nn ca

# commit
git commit

# the commit message is pre-populated as:


Co-authored-by: James Holden <jholden@rocinante.com>
Co-authored-by: Naomi Nagata <nnagata@rocinante.com>
Co-authored-by: Chrisjen Avasarala <avasarala@un.gov>


# soloing
git author ca

# commit
git commit

# the commit message is pre-populated as:


Authored-by: Chrisjen Avasarala <avasarala@un.gov>
```

# Why
`git-together` is a wonderful tool to change the `author` and `commit` fields
in the git commit object, and rotate the authors automatically to evenly
distribute the credit.

However, both the git `author` and `commit` fields may change or be lost in the
future due to merging, rebasing, and cherry-picking.

Also, `git-together` cannot put multiple authors directly into same commit,
e.g. it only supports one `Signed-off-by:` message generated by `git commit
--signoff`.

`git-author` is created to extend the `git-together` capability, so that all
the authorship information will be captured as part of the commit message,
hence, it won't care about who actually tracked in the `author` and `commit`
fields in the git log. 

See this discussion on the open source GPDB project's mailing list:
https://groups.google.com/a/greenplum.org/forum/#!msg/gpdb-dev/qHqa9UbFpSA/u0Y0g2rqAAAJ
