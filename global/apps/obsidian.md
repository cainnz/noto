## Must have plugins 4/1/2023



## Obsidian Git avoid branches/github file conflicts

***when using Obsidian Git and pushing your notes to github, add the following to the .gitignore file***

.gitignore
```bash
.trash/
.DS_Store
.obsidian/ ## this will ignore the .obsidian folder where it contains all plugins files, helps with using too much github space
.obsidian/workspace ## this folder/files causes lots of conflicts issues since I open my obsidian notes in multiple devices
```
**do not forget to commit your changes** 