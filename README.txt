Setup:
Need to downloand maven and extract it.
create env variable M2_HOME to the maven root folder
add M2_HOME/bin to the path system env variable

Maven help:
> mvn -h

Settings:
maven local user specific root is <users>/.m2
in this there is a repository folder which is the local repo for libraries
under .m2/settings.xml can be created to override quite a many settings like:
setting up proxies, local repository, profiles, servers, mirror, etc.,
	
Dependency Management:
if we want to add more remote repsotories, that can be done in settings.xml or in a project's pom.xml
dependencies are defined in dependencies->dependency elements. groupid, artifectid, type, scope.
types of scope are : 
compile (default, for build, test and run)
provided (build and test. but not packages like servlet api)
runtime (not in compile/build. only used in runtime and gets packaged)
test (only for test)
system: hardcoded path system dependencies


Maven install artifect:
If we want to install my local project into the local repository i can use install:install-file plugin:target to do so. after this is done, i can use this as s dependency in my other local projects as a regular dependeny.
mvn install:install-file -DgroupId=com.apress.gswmbook -DartifactId=test -Dversion=1.0.0 -Dfile=C:\apress\gswm-book\chapter3\test.jar -Dpackaging=jar -DgeneratePom=true

Versioning:
It is recommended that Maven projects use the following conventions for versioning:
<major-version>.<minor-version>.<incremental-version>-qualifier
The major, minor, and incremental values are numeric, and the qualifier can have values such as RC, alpha, beta, and SNAPSHOT. Some examples that follow this convention are 1.0.0, 2.4.5-SNAPSHOT, 3.1.1-RC1, and so forth.
The SNAPSHOT qualifier in the project’s version carries a special meaning. It indicates that the project is in a development stage. When a project uses a SNAPSHOT dependency, every time the project is built, Maven will fetch and use the latest SNAPSHOT artifact.

To build a maven package use:
mvn package

To see dependency tree:
mvn dependency:tree

To compile:
mvn compiler:compile

To clean:
mvn clean:clean. or just mvn clean.


Lifecycles:
In maven either we can run some lifecycle phase which executes several pre phases within the lifecycles. each life cycle phase can be mapped to plugin:goal.
we can run a particular lifecycle as:
mvn lifecyclephase

or we can run a goal as
mvn plugin-name:goalname

more from mvn:
[ERROR] Unknown lifecycle phase "build". You must specify a valid lifecycle phase or a goal in the format <plugin-prefix>:<goal> or <plugin-group-id>:<plugin-artifact-id>[:<plugin-version>]:<goal>. Available lifecycle phases are: validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy, pre-clean, clean, post-clean, pre-site, site, post-site, site-deploy. -> [Help 1]

Maven has following 3 default lifecyles
default: handles compiling, packaging, and deployment.
clean: handles the deletion of temp files and the target dir.
site: handles generation of site generation documents and reports.

Default build lifecycle has following phases: validate, compile, test, package, install, deploy.
if we run package, then all phases prior to package are executed in chain till package.

if we want to skip running test phase:
mvn package –Dmaven.test.skip=true


Archetypes:
Archetypes are the project templates which we can use to create the project dires and files as per a template.

mvn archetype:generate will list all the available archetypes and then ask for you to select one. and then it creates

Example:
generate a web project:
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-webapp
above command will interactively ask for mandatory parameters like groupid etc..
 



