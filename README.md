# Ballerina GitHub Connector

###### GitHub brings together the world's largest community of developers to discover, share, and build better software. From open source projects to private team repositories, GitHub is an all-in-one platform for collaborative development.

The Ballerina GitHub connector allow users to access the GitHub API through ballerina. This connector uses the GitHub GraphQL API v4.0

|Ballerina Version | Connector Version |
|------------------|-------------------|
|0.970.0-alpha1-SNAPSHOT | 0.1 |

![Ballerina GitHub Connector Overview](BallerinaGitHubConnector_Overview.jpg)

### Getting started

* Clone the repository by running the following command
```
git clone https://github.com/vlgunarathne/connector-github.git
```
* Import the package to your ballerina project.

##### Prerequisites
Download the ballerina version 0.970.0-alpha1-SNAPSHOT [distribution](https://ballerinalang.org/downloads/).

### Working with GitHub Connector Actions

All the actions return `struct objects` and `github:GitConnectorError`. If the actions was a success, then the requested struct object will be returned while the `github:GitConnectorError` will be **null** and vice-versa.

##### Example
* Request 
```ballerina
    github:GitHubConnector githubConnector = { accessToken: getAccessToken()};
    github:GitConnectorError e = {};
    
    //Get a single repository
    github:Repository repository = {};
    var repo = githubConnector.getRepository("wso2/product-apim");
    match repo {
        github:Repository rep => {
            repository = rep;
            io:println(repository);
        }
        github:GitConnectorError err => {
            io:println(err);
        }
    }
    
```

* Response struct
```ballerina
public struct Repository {
    string id;
    string name;
    string createdAt;
    string updatedAt;
    string description;
    int forkCount;
    boolean hasIssuesEnabled;
    boolean hasWikiEnabled;
    string homepageUrl;
    boolean isArchived;
    boolean isFork;
    boolean isLocked;
    boolean isMirror;
    boolean isPrivate;
    string license;
    string lockReason;
    string mirrorUrl;
    string url;
    string sshUrl;
    RepositoryOwner owner;
    Language primaryLanguage;
}
```

***
## Connector API

### API Reference
- [getRepository()](https://github.com/vlgunarathne/connector-github#getrepository)
    - [getProjectList()](https://github.com/vlgunarathne/connector-github#getprojectlist)
    - [getProject()](https://github.com/vlgunarathne/connector-github#getproject)
    - [getIssueList()](https://github.com/vlgunarathne/connector-github#getissuelist)
    - [getIssue()](https://github.com/vlgunarathne/connector-github#getissue)
    - [getPullRequestList()](https://github.com/vlgunarathne/connector-github#getpullrequestlist)

- [getOrganization()](https://github.com/vlgunarathne/connector-github#getorganization)
    - [getProjectList()](https://github.com/vlgunarathne/connector-github#getprojectlist-1)
    - [getProject()](https://github.com/vlgunarathne/connector-github#getproject-1)
    - [getRepositoryList()](https://github.com/vlgunarathne/connector-github#getrepositorylist)
    
### getRepository()
Return a single repository.

###### Parameters
Name | Type | Description
-----|------|------------
name | string | Name of the organization and repository. (Eg: "organization/repository")

###### Returns
* **github:Repository , github:GitConnectorError**

***

### getOrganization()
Return a single organization.

###### Parameters
Name | Type | Description
-----|------|------------
name | string | Name of the organization. (Eg: "organization")

###### Returns
**github:Organization , github:GitConnectorError**

***
## github:Repository

### getProjectList()
Return a list of projects in the repository.

###### Parameters
Name | Type | Description
-----|------|------------
state | string | The state of the project. (Eg: github:GIT_STATE_OPEN, github:GIT_STATE_CLOSED, github:GIT_STATE_ALL )

###### Returns
**github:ProjectList , github:GitConnectorError**

***
### getProject()
Return a single project of the repository.

###### Parameters
Name | Type | Description
-----|------|------------
projectNumber | int | The integral number of the project.

###### Returns
**github:Project , github:GitConnectorError**

***

### getIssueList()
Return a list of issues of the repository.

###### Parameters
Name | Type | Description
-----|------|------------
state | string | The state of the issue. (Eg: github:GIT_STATE_OPEN, github:GIT_STATE_CLOSED, github:GIT_STATE_ALL )

###### Returns
**github:IssueList , github:GitConnectorError**

***

### getIssue()
Return a single issue of the repository.

###### Parameters
Name | Type | Description
-----|------|------------
issueNumber | int | The integral number of the issue.

###### Returns
**github:Issue , github:GitConnectorError**

***

### getPullRequestList()
Return a list of pull requests of the repository.

###### Parameters
Name | Type | Description
-----|------|------------
state | string | The state of the pull request. (Eg: github:GIT_STATE_OPEN, github:GIT_STATE_CLOSED, github:GIT_STATE_MERGED, github:GIT_STATE_ALL)

###### Returns
**github:PullRequestList , github:GitConnectorError**

***

## github:Organization

### getProjectList()
Return a list of projects on the organization.

###### Parameters
Name | Type | Description
-----|------|------------
state | string | The state of the project. (Eg: github:GIT_STATE_OPEN, github:GIT_STATE_CLOSED, github:GIT_STATE_ALL )

###### Returns
**github:ProjectList , github:GitConnectorError**

***

### getProject()
Return a single project of the organization.

###### Parameters
Name | Type | Description
-----|------|------------
projectNumber | int | The integral number of the project.

###### Returns
**github:Project , github:GitConnectorError**

***

### getRepositoryList()
Return the list of repositories of the organization.

###### Parameters
None

###### Returns
**github:RepositoryList , github:GitConnectorError**

***

## github:Project

### getColumnList()
Return a list of columns in the project.

###### Parameters
None

###### Returns
**github:ColumnList**

***

## github:Column

### getCardList()
Return a list of cards in the column.

###### Parameters
None

###### Returns
**github:CardList**

***
## github:RepositoryList

### getAllRepositories()
Return an array of repositories.

###### Parameters
None

###### Returns
**github:Repository[]**

***

### nextPage()
Return the next page of the repository list.

###### Parameters
None

###### Returns
**github:RepositoryList , github:GitConnectorError**

***

### hasNextPage()
Check if there is another page for the repository list.

###### Parameters
None

###### Returns
**boolean**

***

### hasPreviousPage()
Check if there is a previous page for the repository list.

###### Parameters
None

###### Returns
**boolean**

***

## github:ColumnList

### getAllColumns()
Return an array of columns.

###### Parameters
None

###### Returns
**github:Column[]**

***
### nextPage()
Return the next page of the column list.

###### Parameters
None

###### Returns
**github:ColumnList , github:GitConnectorError**

***
### hasNextPage()
Check if there is another page for the column list.

###### Parameters
None

###### Returns
**boolean**

***

### hasPreviousPage()
Check if there is a previous page for the column list.

###### Parameters
None

###### Returns
**boolean**

***

## github:CardList

### getAllCards()
Return an array of cards.

###### Parameters
None

###### Returns
**github:Card[]**

***

### nextPage()
Return the next page of the card list.

###### Parameters
None

###### Returns
**github:CardList , github:GitConnectorError**

***
### hasNextPage()
Check if there is another page for the card list.

###### Parameters
None

###### Returns
**boolean**

***

### hasPreviousPage()
Check if there is a previous page for the card list.

###### Parameters
None

###### Returns
**boolean**

***
