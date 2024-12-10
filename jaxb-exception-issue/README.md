# Reproducer

Steps are:

```
$ mvn clean package
$ java -jar target/jaxb-exception-issue-0.0.1-SNAPSHOT.jar marshall
```

This will generate `fruit.xml` in the current working directory.

Edit it so that the XML becomes invalid. E.g. change `</n>` to `<n>`.

Try to unmarshall with a non-English locale. For example:

```
$ java -Duser.language=de -Duser.country=DE -Duser.timezone=Europe/Berlin -jar target/jaxb-exception-issue-0.0.1-SNAPSHOT.jar unmarshall
```

This will output something like:

```
MESSAGE = |Elementtyp "n" muss mit dem entsprechenden Endtag "</n>" beendet werden.|
LOCALIZED MESSAGE = |Elementtyp "n" muss mit dem entsprechenden Endtag "</n>" beendet werden.|
```

That is, the localized and non-localized message are **both** localized.
