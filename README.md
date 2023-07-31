# AEM WKND Shared Project

![Maven CI](https://github.com/adobe/aem-guides-wknd-shared/actions/workflows/maven.yml/badge.svg)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.adobe.aem.guides/aem-guides-wknd-shared/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.adobe.aem.guides/aem-guides-wknd-shared)

This is an Adobe Experience Manager project containing shared content and configuration, shared by the various WKND (a fictitious lifestyle brand) applications (WKND Sites, WKND PWA, etc.).

This project is not intended to be installed standalone, rather embedded in other projects that use it's content such as [WKND Site](https://github.com/adobe/aem-guides-wknd).

## What's included

The following content and configuration are included using the app name `wknd-shared`. 

| Location            | Description          | 
|---------------------|----------------------|
| /content/dam/wknd-shared | Image assets and Content Fragments (Article, Adventure, Author) |
| /content/cq:tags/wknd-shared | WKND tags |
| /conf/wknd-shared/settings/dam/cfm/models | Content Fragment Models (Article, Adventure, Author) |
| /conf/wknd-shared/settings/graphql/persistentQueries | Several persistent queries for Adventures and Articles |

## How to use

Add the WKND Shared artifact `ui.content` as a dependency to other WKND project's `all/pom.xml`. The `ui.content` module is used directly to ensure proper package installation based on the dependency chain.

```
<dependencies>
    ...
    <dependency>
        <groupId>com.adobe.aem.guides</groupId>
        <artifactId>aem-guides-wknd-shared.ui.content</artifactId>
        <version>x.x.x</version>
        <type>zip</type>
    </dependency> 
    ...
</dependencies>
```

Then embed the `aem-guides-wknd-shared.ui.content` artifact in the other WKND project's `all/pom.xml`, updating the `<target>` to match the embedding WKND apps' name.

```
<plugins>
    <plugin>
        <groupId>org.apache.jackrabbit</groupId>
        <artifactId>filevault-package-maven-plugin</artifactId>
        ...
        <configuration>
            ...
            <embeddeds>
                ...
                <embedded>
                    <groupId>com.adobe.aem.guides</groupId>
                    <artifactId>aem-guides-wknd-shared.ui.content</artifactId>
                    <type>zip</type>
                    <target>/apps/wknd-vendor-packages/content/install</target>
                </embedded>
                ...
            </embeddeds>
            ...
        </configuration>
        ...
    </plugin>
    ...
</plugins>
```

Add the `aem-guides-wknd-shared.ui.content` as a dependency to other project's `ui.content` module's `filevault-package-maven-plugin` and `dependencies` if the target project depends on WKND Shared content being installed **first**.

```xml
<build>
    <plugins>
        <build>
        <plugins>
            <plugin>
                <groupId>org.apache.jackrabbit</groupId>
                <artifactId>filevault-package-maven-plugin</artifactId>
                <configuration>
                    <group>com.adobe.aem.guides</group>
                    <name>aem-guides-wknd.ui.content</name>
                    <packageType>content</packageType>
                    <accessControlHandling>merge</accessControlHandling>
                    <dependencies>
                        <!-- INCLUDE WKND SHARED DEPENDENCY -->
                        <dependency>
                            <groupId>com.adobe.aem.guides</groupId>
                            <artifactId>aem-guides-wknd-shared.ui.content</artifactId>
                        </dependency>
                    </dependencies>
                </configuration>
            </plugin>
            ...
        </plugins>
    </build>
    ...
    <dependencies>
        ...
        <!-- INCLUDE WKND SHARED DEPENDENCY -->
        <dependency>
            <groupId>com.adobe.aem.guides</groupId>
            <artifactId>aem-guides-wknd-shared.ui.content</artifactId>
            <version>${wknd-shared.version}</version>
            <type>zip</type>
        </dependency>
        ...
    </dependencies>
```


## System Requirements

WKND Shared version | AEM as a Cloud Service | AEM 6.5 | AEM 6.4 | Java SE | Maven
| ---------- | ---------|---------|---------|---------|---------
WKND Shared 3.x | Continual | Not supported| Not supported| 8, 11 | 3.3.9+
WKND Shared 2.x | Continual | 6.5.13+ | Not supported| 8, 11 | 3.3.9+

Setup your local development environment for [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) or for [older versions of AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html).


## Documentation

* This project was generated using the [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html).
