# AEM WKND Shared Project

![Maven CI](https://github.com/adobe/aem-guides-wknd-shared/actions/workflows/maven.yml/badge.svg)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.adobe.aem.guides/aem-guides-wknd-shared/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.adobe.aem.guides/aem-guides-wknd-shared)

This is an Adobe Experience Manager project containing shared content and configuration, shared by the various WKND (a fictitious lifestyle brand) applications (WKND Sites, WKND PWA, etc.).

This project is not intended to be installed standalone, rather embedded in other projects that use it's content such as [WKND Site](https://github.com/adobe/aem-guides-wknd).

## What's included

The following content and configuration are included using the app name `wknd-shared`. 

| Location            | Description          | 
|---------------------|----------------------|
| /content/dam/wknd-shared | Image assets and Content Fragments (Article, Adventure) |
| /content/cq:tags/wknd-shared | WKND tags |
| /conf/wknd-share | Content Fragment Models (Article, Adventure) |

## How to use

Add the WKND Shared artifact as a dependency to other WKND project's `all/pom.xml`. 

```
<dependencies>
    ...
    <dependency>
        <groupId>com.adobe.aem.guides</groupId>
        <artifactId>aem-guides-wknd-shared.all</artifactId>
        <version>1.0.0</version>
        <type>zip</type>
    </dependency>
    ...
</dependencies>
```

Then embed the `aem-guides-wknd-shared.all` artifact in the other WKND project's `all/pom.xml`, updating the `<target>` to match the embedding WKND apps' name.

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
                    <artifactId>aem-guides-wknd-shared.all</artifactId>
                    <type>zip</type>
                    <target>/apps/the-wknd-app-packages/content/install</target>
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

## System Requirements

 AEM as a Cloud Service | AEM 6.5 | AEM 6.4 | Java SE | Maven
---------|---------|---------|---------|---------
Continual | 6.5.7.0+ | 6.4.8.4+ | 8, 11 | 3.3.9+

Setup your local development environment for [AEM as a Cloud Service SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) or for [older versions of AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html).


## Documentation

* This project was generated using the [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html).
