### Vim.gitignore
[._]*.s[a-w][a-z]

[._]s[a-w][a-z]

*.un~

Session.vim

.netrwhist

*~

### GWT.gitignore
*.class

Package Files
*.jar
*.war

gwt caches and compiled units
war/gwt_bree/
gwt-unitCache/

boilerplate generated classes
.apt_generated/

more caches and things from deploy
war/WEB-INF/deploy/
war/WEB-INF/classes/

compilation logs
.gwt/

caching for already compiled files
gwt-unitCache/

gwt junit compilation files
www-test/

old GWT (1.5) created this dir
.gwt-tmp/

### Maven.gitignore
target/
pom.xml.tag
pom.xml.releaseBackup
pom.xml.versionsBackup
pom.xml.next
release.properties
dependency-reduced-pom.xml
buildNumber.properties
.mvn/timing.properties

### Java.gitignore
*.class

Mobile Tools for Java (J2ME)
.mtj.tmp/

Package Files
*.jar
*.war
*.ear

virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml
hs_err_pid*

### Go.gitignore
Compiled Object files, Static and Dynamic libs (Shared Objects)
*.o
*.a
*.so

Folders
_obj
_test

Architecture specific extensions/prefixes
*.[568vq]
[568vq].out

*.cgo1.go
*.cgo2.c
_cgo_defun.c
_cgo_gotypes.go
_cgo_export.*

_testmain.go

*.exe
*.test
*.prof

### Gradle.gitignore
.gradle
build/

Ignore Gradle GUI config
gradle-app.setting

Avoid ignoring Gradle wrapper jar file (.jar files are usually ignored)
!gradle-wrapper.jar

Cache of project
.gradletasknamecache

### JBoss.gitignore
jboss/server/all/deploy/project.ext
jboss/server/default/deploy/project.ext
jboss/server/minimal/deploy/project.ext
jboss/server/all/log/*.log
jboss/server/all/tmp/**/*
jboss/server/all/data/**/*
jboss/server/all/work/**/*
jboss/server/default/log/*.log
jboss/server/default/tmp/**/*
jboss/server/default/data/**/*
jboss/server/default/work/**/*
jboss/server/minimal/log/*.log
jboss/server/minimal/tmp/**/*
jboss/server/minimal/data/**/*
jboss/server/minimal/work/**/*

deployed package files #
*.DEPLOYED

### Python.gitignore
Byte-compiled / optimized / DLL files
__pycache__/
*.py[cod]
*$py.class

C extensions
*.so

Distribution / packaging
.Python
env/
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
*.egg-info/
.installed.cfg
*.egg

PyInstaller
Usually these files are written by a python script from a template
before PyInstaller builds the exe, so as to inject date/other infos into it.
*.manifest
*.spec

Installer logs
pip-log.txt
pip-delete-this-directory.txt

Unit test / coverage reports
htmlcov/
.tox/
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*,cover
.hypothesis/

Translations
*.mo
*.pot

Django stuff:
*.log

Sphinx documentation
docs/_build/

PyBuilder
target/

Ipython Notebook
.ipynb_checkpoints

### Eclipse.gitignore
.metadata
bin/
tmp/
*.tmp
*.bak
*.swp
*~.nib
local.properties
.settings/
.loadpath

Eclipse Core
.project

External tool builders
.externalToolBuilders/

Locally stored "Eclipse launch configurations"
*.launch

PyDev specific (Python IDE for Eclipse)
*.pydevproject

CDT-specific (C/C++ Development Tooling)
.cproject

JDT-specific (Eclipse Java Development Tools)
.classpath

Java annotation processor (APT)
.factorypath

PDT-specific (PHP Development Tools)
.buildpath

sbteclipse plugin
.target

TeXlipse plugin
.texlipse

STS (Spring Tool Suite)
.springBeans

### JetBrains.gitignore
Covers JetBrains IDEs: IntelliJ, RubyMine, PhpStorm, AppCode, PyCharm, CLion, Android Studio and Webstorm

*.iml

Directory-based project format:
.idea/
if you remove the above rule, at least ignore the following:

User-specific stuff:
.idea/workspace.xml
.idea/tasks.xml
.idea/dictionaries
.idea/shelf

Sensitive or high-churn files:
.idea/dataSources.ids
.idea/dataSources.xml
.idea/sqlDataSources.xml
.idea/dynamic.xml
.idea/uiDesigner.xml

Gradle:
.idea/gradle.xml
.idea/libraries

Mongo Explorer plugin:
.idea/mongoSettings.xml

File-based project format:
*.ipr
*.iws

Plugin-specific files:
IntelliJ
/out/

mpeltonen/sbt-idea plugin
.idea_modules/

JIRA plugin
atlassian-ide-plugin.xml

Crashlytics plugin (for Android Studio and IntelliJ)
com_crashlytics_export_strings.xml
crashlytics.properties
crashlytics-build.properties
fabric.properties