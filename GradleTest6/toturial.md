```
hanrong@MyUbuntu:/home$ cd hanrong/
hanrong@MyUbuntu:~$ pwd
/home/hanrong
hanrong@MyUbuntu:~$ cd .gradle/
hanrong@MyUbuntu:~/.gradle$ ls
caches  daemon  gradle.properties  init.gradle  native  workers  wrapper
hanrong@MyUbuntu:~/.gradle$ mv init.gradle  ~
hanrong@MyUbuntu:~/.gradle$ cat ~/init.gradle 
allprojects{
    repositories {
        def ALIYUN_REPOSITORY_URL = 'http://maven.aliyun.com/nexus/content/groups/public'
        def ALIYUN_JCENTER_URL = 'http://maven.aliyun.com/nexus/content/repositories/jcenter'
        all { ArtifactRepository repo ->
            if(repo instanceof MavenArtifactRepository){
                def url = repo.url.toString()
                if (url.startsWith('https://repo1.maven.org/maven2')) {
                    project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_REPOSITORY_URL."
                    remove repo
                }
                if (url.startsWith('https://jcenter.bintray.com/')) {
                    project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_JCENTER_URL."
                    remove repo
                }
            }
        }
        maven {
                url ALIYUN_REPOSITORY_URL
            url ALIYUN_JCENTER_URL
        }
    }
}
```
