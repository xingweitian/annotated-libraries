The Travis jobs that use the Checker Framework download the annotated JDK from
this repository. Which version of the JDK is determined by the commit hash
specified in checker/build.xml.

Therefore, if some pull request changes the annotated JDK, a new version built
using the pull request should be added to this repository.  The pull request
should then update checker/build.xml to use the commit hash of the new version.
If a conflict on this line occurs, then merge master into the pull request and
start over.

More specifically, you should:

1. In the branch that contains your Checker Framework pull request, do:
````
    git pull git@github.com:typetools/checker-framework.git
    ./gradlew buildJdk
````

2. Upload dist/jdk8.jar (or checker/jdk/jdk8.jar, they are the same)
to this repository.  You can do by committing it to
https://github.com/typetools/annotated-libraries or via
https://github.com/typetools/annotated-libraries/upload/master.

3. In the branch that contains your Checker Framework pull request,
in file `jdk8/build.gradle`, in the `downloadJdk` task,
assign the hash of your commit to shaHash.

4. Wait for Travis to successfully build the pull request.

5. If the pull request suffers a merge conflict on the line that contains
the commit hash, then start over at step 1.

5. Merge the pull request.  (Never merge any pull request that does not
pass its tests!)

