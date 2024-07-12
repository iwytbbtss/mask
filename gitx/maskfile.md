# Commands related to Git

## commit

> add . & commit with Type, Scope(Optional), Message

```sh
TYPE=$(gum choose "feat" "fix" "hotfix" "refactor" "chore" "design" "revert" "etc") && \
SCOPE=$(gum input --placeholder "scope");
# wrap it in bracket if it has a value.
test -n "$SCOPE" && SCOPE="($SCOPE)"
test -n "$TYPE" && SUMMARY=$(gum input --value "$TYPE$SCOPE: " --placeholder "commit message")
git add . && \
git commit -m "$SUMMARY"
```

## push

> commit & push for current branch

```sh
source "$MASKFILE_DIR/../.env"
BRANCH=$(git rev-parse --abbrev-ref HEAD)
$MASK commit && \
git push origin $BRANCH && \
echo $SUCCESS_COLOR"Success to Push origin/$BRANCH"$NO_COLOR || \
echo $ERROR_COLOR"Failed to Push origin/$BRANCH"$NO_COLOR
```

## br:c

> create new branch

```sh
NAME=$(gum input --placeholder "branch name");
git switch -c $NAME
```

## br:d

> delete branch (remote too)

```sh
BRANCHES=$(git branch --format="%(refname:short)")
CHOSEN=$(echo "$BRANCHES" | gum choose)
git branch -D $CHOSEN && \
git fetch -p
```

## mgto

> merge current branch to target branch & switch to target branch

```sh
source "$MASKFILE_DIR/../.env"
OTHERS=$(git branch | grep -v "\*")
CHOSEN=$(echo "$OTHERS" | gum choose)
CURRENT=$(git rev-parse --abbrev-ref HEAD)
git switch $CHOSEN && \
git merge $CURRENT --no-edit && \
echo $SUCCESS_COLOR"Success to Switch&Merge $CHOSEN"$NO_COLOR
```
