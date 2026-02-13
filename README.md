# empty_dir

Somewhat [infamously](https://stackoverflow.com/q/115983/3697870), git does not track [empty directories](https://archive.kernel.org/oldwiki/git.wiki.kernel.org/index.php/GitFaq.html#Can_I_add_empty_directories.3F).

The usual workaround is to put *something* in the directory, like a README file or an empty `.gitkeep` file. But sometimes, you really do want an empty folder.

This repo is a demonstration of how to achieve that. It contains a folder called `the_empty_dir` containing a placeholder file. When you clone the repository, you get the directories, including the placeholder file. But simply running `git checkout` will trigger the `post-checkout` hook and remove the placeholder (and any others by the same name). You'll be left with an empty directory, just as the doctor ordered. And you wont be bothered about its disappearance, because it gets flagged with "assume-unchanged".

To prevent untrusted code from executing, git requires the hook to be enabled first. [Since Git 2.9](https://stackoverflow.com/a/37861972/3697870), the easiest way to do that is by executing `git config core.hooksPath .githooks` in your working copy, and then running `git checkout`. Alternatively one of the many shared git hook management techniques, like that enabled by [git-hooks](https://github.com/git-hooks/git-hooks), can be substituted.

Assumedly, you want the empty directory as a starting point for something. So this demonstration also ignores anything you *add* to the directory. You can change that behaviour in `.gitignore`.

If you ever delete the directory, just pull again and it will return.

Note the `post-checkout` hook was selected because there is [no reliable solution](https://stackoverflow.com/a/5623947/3697870) for a post-pull hook. Checkout is a common, non-destructive action that is easy to expect of a user. The hook is also triggered by a `git clone`, so if you have a centralised git hook system like [shared-git-hooks](https://github.com/kilianc/shared-git-hooks), it can simply happen when the repository is first cloned.
