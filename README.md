There are 3 apps : 1- producer app which will send auto-generated messages to rabbitmq 2- rabbitmq app which will handles these messages in a queue and send these messages to the consumer app 3- consumer app is the app that will get the messages after queueing from rabbitmq (in other words - consume messages)

Steps to deploy the chart into github-pages :

1- clone the repo : git clone https://github.com/samer-habash/kubernetes-project-helm-charts

2- The predefined branch from github called gh-pages is specially for pushing helm charts: (checkout to gh-branch) ~ git checkout -b gh-pages

3- create index.yaml file for pushing the helm chart
~ mkdir index ~ touch index/index.yaml ~ git add . ~ git commit -a -m "adding index.yaml" ~ git push --set-upstream origin gh-pages

4- Goto github.com to your repo settings => Options => and scroll down to “GitHub pages” section. Then choose gh-pages branch for the source. Copy the link above to the clipboard.

5- Adding the chart to git hub we need to package the helm : packaging the helm will just convert the repo into .tgz file :

~ helm package rabbitmq-Chart ~ mv rabbitmq-chart-0.1.0.tgz index/ ~ cd index/ ~ helm repo index . --url paste-the-link-from-step-5

NOTE: the helm repo index fulfills the index.yaml file with the corresponding version/url/etc...

6- afterwards you can check your index.yaml which has the info and the description

7- commit and push ~ git commit -a -m "created index.yaml" ~ git push

8- confirm you can get the index.yaml file from curl :
curl https://samer-habash.github.io/kubernetes-project-helm-charts/index/index.yaml

9- add your repo to your helm list directly (note give a name to the repo): 
~ helm repo add <choose-name-repo> paste-the-link-from-step-5/index

in my case example : helm repo add rabbiemq-chart-repo https://samer-habash.github.io/kubernetes-project-helm-charts/index/
NOTE: we added index directory from first in order to save the index and .tgz chart to be on separate directory from the chart code in github

10- Confirm that the repo has been added to your helm list: ~ helm repo list

Thats it !
