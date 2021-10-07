=== "build.gradle.kts"
    ```kotlin
    repositories {
        mavenCentral()
        maven("https://oss.sonatype.org/content/repositories/snapshots/")
    }
    
    dependencies {
        implementation("me.jakejmattson:DiscordKt:0.23.0-SNAPSHOT")
    }
    ```
    
=== "build.gradle"
    ```groovy
    repositories {
        mavenCentral()
        maven {
            url 'https://oss.sonatype.org/content/repositories/snapshots/'
        }
    }
    
    dependencies {
        implementation 'me.jakejmattson:DiscordKt:0.23.0-SNAPSHOT'
    }
    ```
    
=== "pom.xml"
    ```xml
    <repositories>
        <repository>
            <id>Sonatype Snapshots</id>
            <url>https://oss.sonatype.org/content/repositories/snapshots/</url>
        </repository>
    </repositories>
    
    <dependencies>
        <dependency>
            <groupId>me.jakejmattson</groupId>
            <artifactId>DiscordKt</artifactId>
            <version>0.23.0-SNAPSHOT</version>
        </dependency>
    </dependencies>
    ```
    