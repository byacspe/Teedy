pipeline {
agent any

```
tools {
    jdk 'JDK11'
    maven 'Maven3'
}

stages {

    stage('Build') {
        steps {

            bat 'java -version'

            bat 'mvn -version'

            bat 'mvn clean install -Dmaven.test.skip=true -Dmaven.javadoc.skip=true -U'
        }
    }

    stage('Package') {
        steps {
            echo 'Build Success'
        }
    }
}
```

}
