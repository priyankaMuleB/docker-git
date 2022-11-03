pipeline
{
	agent
	{
		label 
		{
			label 'QA'
		}
	}
	stages
	{
		stage('checkout')
		{
			steps
			{
				sh '''
					rm -fr *
					sudo yum install git -y
					git init
					git clone https://github.com/priyankaMuleB/docker-git.git
					cd docker-git
					git checkout 22Q1
					sudo docker kill myhttpd-85 myhttpd-90 myhttpd-8081
					sudo docker system prune -a -f
					sudo docker run -itdp 85:80 --name myhttpd-85 httpd
					sudo chmod 777 index.html
					sudo docker cp index.html myhttpd-85:/usr/local/apache2/htdocs
					git checkout -f 22Q2
					sudo docker run -itdp 90:80 --name myhttpd-90 httpd
					sudo chmod 777 index.html
					sudo docker cp index.html myhttpd-90:/usr/local/apache2/htdocs
					git checkout -f 22Q3
					sudo docker run -itdp 8081:80 --name myhttpd-8081 httpd
					sudo chmod 777 index.html
					sudo docker cp index.html myhttpd-8081:/usr/local/apache2/htdocs
				'''
			}
		}	
	}
}
