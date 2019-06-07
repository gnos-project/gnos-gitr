# GNOS gitr

Initialize GIT repos, configure remotes, branch tracking & networking options.

- Local repo creation & configuration
- Remote repo creation (see backends)
- `git pa` to push to **all** remotes
- `git pull` to pull from **first** remote
- **TOR** & SOCKS support

## Usage

```
gitr \
    --tor     9050 \
    --key     path/to/ssh_key \
    --name    "My git name" \
    --email   my_git@email.tld \
    --github  user/repo[%public][@branch] \
    --keybase user/repo[%teamid][@branch] \
    --gitlab  [git@my-gitlab.tld[:22]:]user/repo[@branch] \
    --ssh     user@my-server.tld[:222]:path/repo[@branch] \
    REPO_PATH@BRANCH_NAME
```

## Pluggable backends

|  BACKEND  |       CREATION       |    Supported SCOPES   | KEY | TOR |
|===========|======================|=======================|=====|=====|
| ssh       | `ssh git init`       | private               | yes | yes |
| gitlab    | `git push`           | private               | yes | yes |
| github    | API prompts password | private,public        | yes | !!! |
| bitbucket | API prompts password | private,public,TEAMID | yes | yes |
| keybase   | CLI may call GUI     | private,TEAMID        | no  | no  |



<!-- TODO Gitlab python CLI
| gitlab_cli | CLI requires config+token | private,public,internal | yes | yes |
 -->

### SSH

Will never support scopes.

Repo creation is scripted over ssh.

### Gitlab

Does not support scopes yet.

Automatic repo creation handled by pushing to a non-existent repo.

### Github

While pushing over TOR seems ok, using Github API to create repos over TOR leads to getting your account flagged, don't do it, create your repo *manually* before pushing (use Tor Browser) !

BUG: Private repos cannot be checked

### Bitbucket

NOT TESTED YET !!!

BUG: Private repos cannot be checked

### Keybase

Does not support TOR yet.

Will never support SSH keys.

## Roadmap

- Fix Github/Bitbucket private repo checks
- Implement Gitlab API to support public/internal scopes, will require tokens
- Implement Keybase [TOR support](https://keybase.io/docs/command_line/tor)
- Implement Gitlab/Github/Bitbucket repo description/tags
- Implement SSH key upload (`ssh-copy-id`, APIs)
