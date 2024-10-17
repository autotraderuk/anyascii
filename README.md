# AnyAscii with Allowlist

This is a fork of the [AnyAscii project](https://github.com/anyascii/anyascii), which has been extended to let a user supply an allowlist of unicode code points which will not be transiliterated.

## Implementations

The original [AnyAscii project](https://github.com/anyascii/anyascii) supports many languages, the allowlist extention has currently only been implemented for the following languages.

### Java

```java
// Transliterate all unicode code points
String s = AnyAscii.transliterate("€£₱₺");
assert s.equals("EURLPTL");

// Allow some unicode code points
Set<Integer> allowlist = new HashSet<>();
allowlist.add(Character.codePointAt("£", 0));
allowlist.add(Character.codePointAt("₱", 0));
StringBuilder dst = new StringBuilder();
AnyAscii.transliterate("€£₱₺", dst, allowlist);
String s = dst.toString();
assert s.equals("EUR£₱TL");
```

## Publishing

Currently this fork has only been published to a private repository for use in autotraderuk. The mechanism to do so for each implementation is detailed below. Currently artifacts are published from developers machines. Versions follow the format of `upstream-anyascii-version.x`. E.g, for builds of this fork based on version `0.3.2` of the original [AnyAscii project](https://github.com/anyascii/anyascii), sequential versions would be `0.3.2.0`, `0.3.2.1`, `0.3.2.2` etc.


### Java

If required, update the version number in `./impl/java/pom.xml`. From the `./impl/java` directory, run the following command:

```bash
mvn deploy -DaltDeploymentRepository=releaseRepository::default::<repository url> -f pom.xml
```

The `<repository url>` can include any required authentication by using the following format:

```
https://some-username:some-password@some-server.com/path/to/repository
```

## Public publishing

If the original [AnyAscii project](https://github.com/anyascii/anyascii) chooses not to accept [the allowlist PR](https://github.com/anyascii/anyascii/pull/22), we may choose to publish this fork to a public repository. In order to do that we would have to make the following changes:

- Change the repo name, project names, artifact names, etc, to `anyascii-with-allowlist`
- Change root packages to `uk.co.autotrader`
- Set up a CI pipeline which will build, test and publish artifacts
