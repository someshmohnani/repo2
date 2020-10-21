pipeline
{
	tools
	{
		jdk 'myjava'
		maven 'mymaven'
	}
	agent any
	stages
	{
		stage('CodeCompile')
		{
			steps
			{
				sh 'mvn compile'
			}
		}
		stage('CodeReview')
		{
			steps
			{
				sh 'mvn pmd:pmd'
			}
			post
			{
				success
				{
					pmd pattern:target/pmd.xml
				}
			}
		}
		stage('UnitTest')
		{
			steps
			{
				sh 'mvn test'
			}
			post
			{
				success
				{
					junit testResults:target/surefire-reports/*.xml
				}
			}
		}
		stage('MetricCheck')
		{
			steps
			{
				sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
			}
		}
		stage('Package')
		{
			steps
			{
				sh 'mvn package'
			}
		}
	}
}
