# 喷气脑

## issues

- [ ] text clustered when [resizing the terminal window](https://youtrack.jetbrains.com/issue/IDEA-210741). Currently runs 2020.3, seems better. 2022.1, better now. 
- [ ] [repeat action or macro x times](https://intellij-support.jetbrains.com/hc/en-us/community/posts/207028955-Repeat-action-macro-x-times-)
- [ ] [statusbar position information enhancement](https://youtrack.jetbrains.com/issue/IDEA-51897)
- [ ] [the selected keyboard layout get ignored](https://stackoverflow.com/questionws/16623189/intellij-ignores-the-selected-keyboard-layout)
- [ ] create a file named `template.json`, type some standard json data, it says **json property not allowed**

---

- [x] can not select the \&quot;
- [x] [could not find or load main class?](https://stackoverflow.com/a/45911888/11844003) delete the `.idea` folder and reopen the project
- [x] [losing the cursor in the editor](https://intellij-support.jetbrains.com/hc/en-us/community/posts/360004205240-Idea-2019-2EAP-losing-the-cursor-in-the-editor) 可以尝试重启然后等一下
- [x] `$` not resolved, [download Typescript community stubs](https://youtrack.jetbrains.com/issue/WEB-10908?_ga=2.258793354.1476422490.1606371561-260943399.1597912158)
- [x] reader mode option, [uncheck "Redered documentation comments"](https://youtrack.jetbrains.com/issue/IDEA-257800?_ga=2.18994936.1979502551.1610418583-859964968.1608606819)
- [x] [not any combination of gradle/IDE-android-plugin/android-gradle-plugin is valid](https://youtrack.jetbrains.com/issue/IDEA-233929#focus=Comments-27-4020873.0-0)
- [x] atom material icons plugin version34 in IDEA, big bundle size "The plugin update is pending JetBrains approval"
- [x] [Add option to select Recursive "Jars Directory"](https://youtrack.jetbrains.com/issue/IDEA-40818?_ga=2.163901055.1544042630.1611536530-859964968.1608606819)
- [x] [backslash is duplicated in md preview](https://youtrack.jetbrains.com/issue/IDEA-258719) fixed in the 2021.1 EAP

- [x] [recursive call gutter icon not showing up in some circumstance](https://youtrack.jetbrains.com/issue/IDEA-282955) the jetbrains-team answered with

  > in the functional expression or anonymous class, the "recursive" method can be invoked later or even not invoked at all, thus there is no recursive mark on gutter in such cases

---

- [dont collapsing imports](https://stackoverflow.com/questions/3348816/intellij-never-use-wildcard-imports)

- [JavaFX isn't available in AS bundled JDK](https://stackoverflow.com/questions/53903641/where-is-android-studio-markdown-support-plugin-preview-preference#comment95259036_53903641)

- [adding global libraries](https://stackoverflow.com/a/25285102/11844003)

- [directories used for settings](https://intellij-support.jetbrains.com/hc/en-us/articles/206544519-Directories-used-by-the-IDE-to-store-settings-caches-plugins-and-logs)

- [u can't change the gradle version in the template]('https://intellij-support.jetbrains.com/hc/en-us/community/posts/360009175120-Gradle-version-outdated-when-creating-a-new-Project?page=1#community_comment_360001872879')

- [date and time format for live template](https://stackoverflow.com/questions/8714779/is-there-a-shortcut-for-inserting-date-time-in-intellij-idea)

- add [custom tags in tml](https://stackoverflow.com/questions/27211337/adding-custom-html-tags-to-intellij)

- [enable DBMSOUTPUT](https://stackoverflow.com/questions/49606889/use-dbms-output-put-line-in-datagrip-for-sql-files)

- the option `dynamic.classpath` controls how classpath is passed to the JVM: via the command line, or via a file. Most operating systems have maximum command line limit, when it's exceeded, IDEA will not be able to run your application. [check also](https://stackoverflow.com/questions/6381213/idea-10-5-command-line-is-too-long)

- [locked by transaction - oracle intellij client?](https://stackoverflow.com/questions/32815953/locked-by-transaction-consoleoracle-intellij-client) disconnect from the database, and then re-connect (you might also try the rollback button if re-connect not working). check also another answer.

- [change vm options and others](https://serpro69.medium.com/boosting-performance-of-intellij-idea-and-the-rest-of-jetbrains-ides-cd34952bb978) [check also](https://www.oracle.com/java/technologies/javase/vmoptions-jsp.html)

- [change errors and warning reports settings](https://stackoverflow.com/a/44758847/11844003)

- [it stopped analyzing?](https://youtrack.jetbrains.com/issue/IDEA-247329) check the `idea.log` (Help | Collect Logs and Diagnostic Data)

## frequently used keymap

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>V</kbd> paste from history
- <kbd>Shift</kbd> + <kbd>Esc</kbd> hide active tool window
- You can narrow down the list of code completion suggestions by using camel case prefixes. E.g., `throw new NPE`
- u can have multiple carets: press and hold <kbd>Shift</kbd> + <kbd>Alt</kbd> and then click at different positions to set additional carets in the editor
- use <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Alt</kbd> + <kbd>U</kbd> to show the UML diagram
- use <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Alt</kbd> + <kbd>E</kbd> to see recent location (custom shortcut)
- use <kbd>Shift</kbd> + <kbd>Alt</kbd> + <kbd>C</kbd> to see recent changes
- use <kbd>Alt</kbd> + <kbd>Insert</kbd> within the POM or the `build.gradle` file to search dependencies
