Common Project Release Parent Pom
=====================================
[![Maven central](https://maven-badges.herokuapp.com/maven-central/com.github.jerrymice/common/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.github.jerrymice.common/common-pom)
[![License](http://img.shields.io/:license-apache-brightgreen.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)

        this common pom file,may project parent pom,
        avoid the hassle of repeatedly configuring many maven plugin,
        It can help you quickly publish projects to GitHub and Maven Central Repository or Private Nexus Repository.

Reference to current project examples:

	 <paerent>
		<groupId>com.github.jerrymice.common</groupId>
		<artifactId>common-pom</artifactId>
		<version>0.0.2.beta1</version>
	</paerent>

Before use this pom profile,you need config maven setting.xml

    1.setting.xml sonatype-repository config:

        <server>
                <id>sonatype-release</id>
                <username>your sonatype repository username</username>
                <password>your sonatype repository password</password>
        </server>

    2.setting.xml gpg passphrase config:

        <server>
                <id>gpg.passphrase</id>
                <passphrase>password with you generate gpg key</passphrase>
        </server>

Release project into Maven Central Repository command line:

	1.release prepare command line examples:

			mvn release:prepare
				-DreleaseVersion=0.0.2.beta2
				-DdevelopmentVersion=0.0.2.beta3-SNAPSHOT
				-Dtag=common-pom.0.0.2.beta2
				-P public-release

	   if your project include child module,you need use command line

			mvn release:prepare-with-pom
				-DreleaseVersion=0.0.2.beta2
				-DdevelopmentVersion=0.0.2.beta3-SNAPSHOT
				-Dtag=common-pom.0.0.2.beta2
				-P public-release

	2.next:release perform command line examples:

			mvn release:perform -P public-release

You can override properties property value, update default version or configuration value in your project, if you need do it.
    examples:

			<!--used maven-nexus-stging-plugin new version-->
			<maven.nexus-staging.plugin.version>1.6.8</maven.nexus-staging.plugin.version>

			<!--override maven-nexus-stging-plugin autoReleaseAfterClose configuration value->
			<maven.nexus-staging.plugin.autoReleaseAfterClose>false</maven.nexus-staging.plugin.autoReleaseAfterClose>
Your project can deploy nexus repository,your need modify maven settings.xml

    1.maven settings.xml config:
             <server>
                 <id>nexus-release</id>
                  <username>deployment</username>
                  <password>password</password>
             </server>

             </profiles>
                <profile>
                  <properties>
                    <nexus.repository.snapshots.url>http://192.168.1.101:8091/nexus/content/repositories/snapshots/</nexus.repository.snapshots.url>
                    <nexus.repository.releases.url>http://192.168.1.101:8091/nexus/content/repositories/releases/</nexus.repository.releases.url>
                  </properties>
                  <activation>
                    <activeByDefault>true</activeByDefault>
                  </activation>
                </profile>
              </profiles>

    2.run command line deploy project into nexus repository:

        mvn deploy -P nexus-releases
More docs:

   [Maven](http://maven.apache.org/users/index.html)

   [Maven-release-plugin](http://maven.apache.org/maven-release/maven-release-plugin)

   [Nexus-staging-maven-plugin](http://#)

