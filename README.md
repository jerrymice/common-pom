This common pom file,may project parent pom,
avoid the hassle of repeatedly configuring many maven plugin,
It can help you quickly publish projects to GitHub and central repository.

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

Release project to Maven Central Repository command line:

	1.release prepare command line examples:

			mvn release:perpare
				-DreleaseVersion=0.0.2.beta2
				-DdevelopmentVersion=0.0.2.beta3-SNAPSHOT
				-Dtag=common-pom.0.0.2.beta2
				-P public-release

	   if your project include child module,you need user common line

			mvn release:prepare-with-pom
				-DreleaseVersion=0.0.2.beta2
				-DdevelopmentVersion=0.0.2.beta3-SNAPSHOT
				-Dtag=common-pom.0.0.2.beta2
				-P public-release

	2.next:release perform common line examples:

			mvn release:perform -P public-release

You can override properties property value, update default version or configuration value in your project, if you need do it.
   	 examples:

			<!--used maven-nexus-stging-plugin new version-->
			<maven.nexus-staging.plugin.version>1.6.8</maven.nexus-staging.plugin.version>

			<!--override maven-nexus-stging-plugin autoReleaseAfterClose configuration value->
			<maven.nexus-staging.plugin.autoReleaseAfterClose>false</maven.nexus-staging.plugin.autoReleaseAfterClose>
More docs:

	Maven

	Maven-release-plugin

	Maven-nexus-stging-plugin

