# empty_dir

**STATUS:** This demonstration was not successful, due to [no reliable solution](https://stackoverflow.com/a/5623947/3697870) for a post-pull hook.

Somewhat [infamously](https://stackoverflow.com/q/115983/3697870), git does not track [empty directories](https://archive.kernel.org/oldwiki/git.wiki.kernel.org/index.php/GitFaq.html#Can_I_add_empty_directories.3F).

The usual workaround is to put *something* in the directory, like a README file or an empty `.gitkeep` file. But sometimes, you really do want an empty folder.

This repo is a demonstration of how to achieve that. It contains a folder called `the_empty_dir` containing a placeholder file. But when you clone it the repository, the `post-merge` hook will run and remove the placeholder (and any others by the same name). You'll be left with an empty directory, just as the doctor ordered. And you wont be bothered about its disappearance, because it is ignored by `.gitignore`.

Assumedly, you want the empty directory as a starting point for something. So this demonstration also ignores anything you *add* to the directory. You can change that behaviour in `.gitignore`.

If you ever delete the directory, just pull again and it will return.
