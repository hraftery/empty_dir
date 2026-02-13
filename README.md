# empty_dir

## tl;dr

Store empty directories in your git repositories by adding a `gitkeep` file to them. The githook will remove the files on next checkout, leaving you with *really* empty directories.

## Say what now?

Somewhat [infamously](https://stackoverflow.com/q/115983/3697870), git does not track [empty directories](https://archive.kernel.org/oldwiki/git.wiki.kernel.org/index.php/GitFaq.html#Can_I_add_empty_directories.3F).

The usual workaround is to put *something* in the directory, like a README or an empty `.gitkeep` file. But sometimes, you really do want an empty folder.

This repo is a demonstration of how to achieve that. It contains a folder called `the_empty_dir` containing a placeholder file. When you clone the repository you get the directory, including the placeholder file. But simply running `git checkout` will trigger the `post-checkout` hook and remove the placeholder. You'll be left with an empty directory, just as the doctor ordered. And you wont be bothered about its disappearance, because it also gets flagged with "assume-unchanged".

Assumedly, you want the empty directory as a starting point for something. So this demonstration also ignores anything you *add* to the directory. You can change that behaviour in `.gitignore`.

## Example usage

1. Add the `.githooks` folder to your repository.
1. Add a directory you want to be empty, and include a file called `gitkeep` in it. The contents don't matter but the filename does.
1. Commit and push your changes.
1. The next time you or someone else pulls the repository, they'll get the directory with the placeholder.
1. Simply execute `git checkout` to remove the placeholders.
    - To prevent untrusted code from executing, git requires the hook to be enabled first. [Since Git 2.9](https://stackoverflow.com/a/37861972/3697870), the easiest way to do that is by executing `git config core.hooksPath .githooks` in your working copy, before running `git checkout`. Alternatively one of the many shared git hook management techniques, like that enabled by [git-hooks](https://github.com/git-hooks/git-hooks), can be substituted.
1. If you ever delete the directory, just `git reset --hard` and it will return.

## Other notes

You're free to repeat this technique anywhere in the repository. As long as the file is named "gitkeep", the same treatment is applied. The name was chosen to be clear in purpose, but still distinct from ".gitkeep" to avoid clashing with existing use.

The `post-checkout` hook was selected because there is [no reliable solution](https://stackoverflow.com/a/5623947/3697870) for a post-pull hook. Checkout is a common, non-destructive action that is easy to expect of a user. The hook is also triggered by a `git clone`, so if you have a centralised git hook system like [shared-git-hooks](https://github.com/kilianc/shared-git-hooks), it can simply happen when the repository is first cloned.

Further discussion on Stack Overflow: https://stackoverflow.com/a/79888529/3697870
