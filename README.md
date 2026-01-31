# 1970 Script - Backdate GitHub Commits
Generate commits with historical timestamps to visualize past contributions on your GitHub profile.

<img width="1883" height="872" alt="image" src="https://github.com/user-attachments/assets/eff104ab-c724-4430-a7e0-27ae9dbd7d80" />
<img width="1128" height="380" alt="image" src="https://github.com/user-attachments/assets/2fa65422-231b-428a-943f-87fc4d0345ab" />


## Table of Contents
- [Travel Back](#travel-back)
- [Explanations](#explanations)
- [Scripts](#scripts)
  - [index.sh](#indexsh)
  - [index2.sh](#index2sh)
  - [index3.sh](#index3sh)
- [Prerequisites](#prerequisites)


## Travel Back

[Create a new repo](https://github.com/new) named `test-commit-in-1970` on GitHub.

[Generate a personal access token](https://github.com/settings/tokens/new) on GitHub and copy it.

Run the following script

```bash
$ sh -c "$(curl -fsSL https://raw.github.com/EsmailEbrahim/1970-script/master/scripts/index.sh)"
```

Enter your GitHub username and access token and then you are done :)

> ⚠️ **Security Note:** This script uses a Personal Access Token. Use a temporary token with minimal permissions and delete it after use.

> The script force-pushes (-f) to ensure the backdated commit is applied correctly to a fresh repository.

## Explanations

This project works because of the way `git` records commits. Whenever you commit something, `git` puts a `Unix timestamp` on it to record when you committed it. A [`Unix timestamp`](https://www.unixtimestamp.com/) is the way computers store the current time. A `Unix timestamp` is a `32-bit` number which stores the number of seconds that has passed from January 1st, 1970 at UTC, the `Unix Epoch`.

The script firstly creates a directory with the name of the wanted year - `line 12` `mkdir $YEAR`

The script then initializes the directory as a git repository, using `git init` - `line 15` `git init`

The script then stages all the files `git add .` and commits it, using the date `{YEAR}-01-01T18:00:00` (`line 25`) or `6pm, 1st January, 1970` (default of the `YEAR` variable)

This is the `ISO Date-Time format` for storing time: `YYYY-MM-DDTHH:MM:SS`.

This commit is then pushed to GitHub (provided you already have made a repository) using `git push -u origin main -f`, and the directory is removed.

GitHub recognizes the commit to have been created at `6 pm, 1st January, 1970` and thus registers a contribution at that moment in time. If you scroll to the first year on your profile, you will see there is a single contribution to your `1970` repository, on 1st January.


## Scripts

### `index.sh`
Generates a single commit backdated to 1970. Useful for testing a single-year contribution.

### `index2.sh`
Creates multiple commits in 1970 to simulate a full year of Git history.

### `index3.sh`
Generates a multi-year timeline (1970–2026) where each commit represents a historical tech milestone.


## Prerequisites
- Git installed on your system
- Basic terminal/bash knowledge
- A GitHub personal access token (with `repo` permission for private repos or `public_repo` for public repos)
