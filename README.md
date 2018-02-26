# Commit messages guide

A guide to understand the importance of commit messages and how to write them well.

It may help you to learn what a commit is, why is it important to write good messages, best practices and some tips to plan and (re)write a good commit history.

## Available languages

- [English](README.md)

## What is a "commit"?

In a simple and roughly way, a commit from is a kind of a _snapshot_ of your local files, written in your local repository.
Contrary to what some people think, [git doesn't store only the difference between the files, it stores a full version of all files](https://git-scm.com/book/eo/v1/Ekkomenci-Git-Basics#Snapshots,-Not-Differences).
For files that didn't change from a commit to another, git stores just a link to the previous identical file that is already stored.

The image bellow show how git stores data over time, in which each "Version" is a commmit:

![](https://i.stack.imgur.com/AQ5TG.png)

## Why commit messages are important?

- To speed up and make easy code reviews
- To help in the understanding of a change
- To explain "the whys" that cannot be described only with code
- To help future maintainers to figure out why and how the changes were made, making easy troubleshooting and debug

To maximize those outcomes, we can use some good practices and standards described in the next section.

## Good practices

These are some practices collected from my experience, aswell from internet articles and other guides. If you have others (or disagree with some) feel free to open a Pull Request and contribute.

### Use imperative form

```
# Good
Use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
Used InventoryBackendPool to retrieve inventory backend
```

_But why use it in the imperative form?_

A commit message describes what the referring change actually **does**, its effects, not what was done.

[This excellent article from Chris Beams](https://chris.beams.io/posts/git-commit/) gives us a simple sentence that can be used to help us write better commit messages and in imperate form:

```
If applied, this commit will <commit message>
```

Examples:

```
# Good
If applied, this commit will use InventoryBackendPool to retrieve inventory backend
```

```
# Bad
If applied, this commit will used InventoryBackendPool to retrieve inventory backend
```

### Capitalize the first letter

```
# Good
Add `use` method to Credit model
```

```
# Bad
add `use` method to Credit model
```

The reason that the first letter should be capitalized is to follow the grammar rule of using capital letters at the beginning of sentences.

The use of this practice may very from person to person, team to team, or even from language to language.
Capitalized or not, an important point is to stick to a single standard and follow it.

### Try to communicate what the change does without having to look at the source code

```
# Good
Add `use` method to Credit model

```

```
# Bad
Add `use` method
```

```
# Good
Increase left padding between textbox and layout frame
```

```
# Bad
Adjust css
```

It is useful in many scenarios (e.g., multiple commits, several changes and refactors) to help reviewrs understand what the committer was thinking.

### Use the message body to explain "why", "for what", "how" and additional details

```
# Good
Fix method name of InventoryBackend child classes

Classes derived from InventoryBackend were not
respecting the base class interface.

It worked because cart was calling the backend implementation
incorrectly.
```

```
# Good
Serialize and deserialize credits to json in Cart

Convert the Credit instances to dict for two main reasons:

  - Pickle relies on file path for classes and we do not want to break up
    everything if a refactor is needed
  - Dict and built-in types are picklable by default
```

```
# Good
Add `use` method to Credit

Change from namedtuple to class because we need to
setup a new attribute (in_use_amount) with a new value
```

The subject and the body of the messages are separated by a blank line.
Additional blank lines are considered as a part of the message body.

Characters like `-`, `*` and \` are elements that improve readability.

## Contributing

Any kind of help would be appreciated. Example of topics that you can help me with:

- Grammar and spelling corrections
- Translation to other languages
- Improvement of source referencing

## Inspirations, sources and further reading

- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
