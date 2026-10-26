# Nexus API

# Queries overview
## get all repos
```bash
curl -u user:pw -X GET 'http://IP:8081/service/rest/v1/repositories'
```
returning the list of repos depending on the user rights

## get all components of a repo
```bash
curl -u user:pw -X GET 'http://IP:8081/service/rest/v1/components?repository=maven-snapshots'
```
returning all the components of the repo

## get one component
```bash
curl -u user:pw -X GET 'http://IP:8081/service/rest/v1/components/bWF2ZW4tc25hcHNob3RzOjhkMTJlNzI'
```
returning the component's assets

## get all releases
```bash
curl -u user:pw -X GET 'http://IP:8081/service/rest/v1/components?repository=maven-releases'
```
returning all the releases of the repo


