# jigsaw test

# setup

1. Download Jdk9 Early Build with Project Jigsaw from https://jdk9.java.net/jigsaw/ and unpack it in ~/bin/java9
2. `export PATH=~/bin/java9/Contents/Home/bin:$PATH`

#examples

## compiling modules

1. `rm -rf mods/*`
2. `rm -rf mods/org.fenixedu.foo && mkdir mods/org.fenixedu.foo && javac -d mods/org.fenixedu.foo $(find org.fenixedu.foo/src -name '*.java')`
3. `rm -rf mods/org.fenixedu.bar && mkdir mods/org.fenixedu.bar && javac -modulepath mods/ -d mods/org.fenixedu.bar $(find org.fenixedu.bar/src -name '*.java')`

## creating module jars

1. `rm -rf mlib && mkdir mlib`
2. `jar --create --file mlib/foo.jar -C mods/org.fenixedu.foo .`
3. `jar --create --file mlib/bar.jar --main-class org.fenixedu.bar.gamma.Gamma -C mods/org.fenixedu.bar .`

# running module
1. `java -mp mlib -m org.fenixedu.bar`

## linking
1. `rm -rf myimage`
2. `export JDKMODS=~/bin/java9/Contents/Home/jmods/`
3. `jlink --modulepath $JDKMODS:mlib --addmods org.fenixedu.bar --output myimage`

## show image modules
1. `myimage/bin/java -listmods`
