pipeline
{
	tools
	{
		jdk 'myjava'
		maven 'mymaven'
	}
	agent none
	stages
	{
		stage('CodeCompile')
		{
			agent any
			steps
			{
				sh 'mvn compile'
			}
		}
		stage('CodeReview')
		{
			agent any
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
			agent any
			steps
			{
				sh 'mvn test'
			}
			post
			{
				success
				{
					junit testResults:'target/surefire-reports/*.xml'
				}
			}
		}
		stage('MetricCheck')
		{
			agent any
			steps
			{
				sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
			}
		}
		stage('Package')
		{
			agent {label 'win_slave'}
			steps
			{
				sh 'mvn package'
			}
		}
	}
}
