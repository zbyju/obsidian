https://cbea.ms/git-commit/

7 Rules to follow:
1. [Separate subject from body with a blank line](https://cbea.ms/git-commit/#separate)
2. [Limit the subject line to 50 characters](https://cbea.ms/git-commit/#limit-50)
3. [Capitalize the subject line](https://cbea.ms/git-commit/#capitalize)
4. [Do not end the subject line with a period](https://cbea.ms/git-commit/#end)
5. [Use the imperative mood in the subject line](https://cbea.ms/git-commit/#imperative)
6. [Wrap the body at 72 characters](https://cbea.ms/git-commit/#wrap-72)
7. [Use the body to explain _what_ and _why_ vs. _how_](https://cbea.ms/git-commit/#why-not-how)

## 1. Subject line
First line will be treated by many tools as the header and it should summarize the commit and what it does.

## 2. Max 50 chars
Not a hard limit but it is recommended. GitHub truncates the subject line after 72 chars with '...' so that should be the hard limit

## 3. Capitalize subject line
Start with a capital letter

## 4. Don't end with a period
Save space by not using '.'

## 5. Use imperative
The git tooling is following this on every occasion and so we should follow (Merge pull request xxx, etc.)

The message should always be able to complete the following sentence:
`If applied, this commit will X`
For example:
`If applied, this commit will`**`refactor subsytem X f`**
