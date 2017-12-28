# Build Info Extractor for gradle problems

Requisite (customize and put it in you `gradle.properties` for example)

    artifactory_user=MY_CUSTOM_USER
    artifactory_password=MY_ARTIFACTORY_TOKEN
    artifactory_contextUrl=MY_ARTIFACTORY_ENDPOINT


## Advanced property customization does not work

execute `./gradlew build aP`

    > Task :artifactoryPublish
    Deploying artifact: http://MY_ARTIFACTORY_HOST/artifactory/libs-snapshot-local/ru/alfalab/platform/tests/sub0/0.1.1-SNAPSHOT/sub0-0.1.1-SNAPSHOT.jar
    Deploying artifact: http://MY_ARTIFACTORY_HOST/artifactory/libs-snapshot-local/ru/alfalab/platform/tests/sub0/0.1.1-SNAPSHOT/sub0-0.1.1-SNAPSHOT.pom
    Deploying artifact: http://MY_ARTIFACTORY_HOST/artifactory/libs-snapshot-local/ru/alfalab/platform/tests/sub1/0.1.1-SNAPSHOT/sub1-0.1.1-SNAPSHOT.jar
    Deploying artifact: http://MY_ARTIFACTORY_HOST/artifactory/libs-snapshot-local/ru/alfalab/platform/tests/sub1/0.1.1-SNAPSHOT/sub1-0.1.1-SNAPSHOT.pom
    Deploying build descriptor to: http://MY_ARTIFACTORY_HOST/artifactory/api/build
    Build successfully deployed. Browse it in Artifactory under http://MY_ARTIFACTORY_HOST/artifactory/webapp/builds/test/1514463347937

And show me properties in artifactory:

    http http://MY_ARTIFACTORY_HOST/artifactory/api/search/gavc g==ru.alfalab.platform.tests a==sub0 repos==libs-snapshot-local X-Result-Detail:properties

    {
        "results": [
            {
                "properties": {
                    "aa": [
                        "aaa"
                    ],
                    "build.name": [
                        "test"
                    ],
                    "build.number": [
                        "1514462774697"
                    ]                        <-------------- where is not_added_prop?
                },
                "uri": "http://.../sub0-....jar"
            },
            {
                "properties": {
                    "aa": [
                        "aaa"
                    ],
                    "build.name": [
                        "test"
                    ],
                    "build.number": [
                        "1514462774697"
                    ],
                    "want_to_add": [           <------------ why only in pom artifacts?
                        "but not"
                    ]
                },
                "uri": "http://.../sub0-....pom"
            }
        ]
    }


I have a question!

1. where is  my `not_added_prop` on sub0 and sub1 jars?
2. why `want_to_add` was added only to pom artifacts?

