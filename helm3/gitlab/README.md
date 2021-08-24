# 简介 

`gitlab-5.2.0.tgz`是从`https://charts.gitlab.io/`下载的.


# 临时记录

```bash
helm3 template --generate-name gitlab/ --set global.hosts.domain=gitlab.jiangtao.com \
    --set certmanager-issuer.email=vlan945@163.com --debug | grep image: > gitlab-helm-image

work_dir=gitlab/helm3/gitlab-5.2.0.tgz
mkdir -p $work_dir
cd $work_dir
for line in $(cat gitlab-helm-image  | sed 's/"//g' | awk '{print $2}' | sort -u );do 
	dir_name=${work_dir}/$(echo $line | awk -F: '{print $1}' | awk -F/ '{print $NF}')
	echo -e "FROM $line\nMAINTAINER Jiangtao <vlan945@163.com>" > $dir_name/Dockerfile
done
```

