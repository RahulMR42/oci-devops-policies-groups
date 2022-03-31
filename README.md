Sample illustrations of `dynamic groups` and `policies` requirements for `OCI Devops`.

----------

### User Groups

<summary>Devops Pipeline (OCI Repo + Build + Deploy) - Click to expand</summary>

-  Create a user and all the devops users to the user group (One group is minimum).
-  You may use `Administrator` group for devops ,however better to create a specific user group to have better control.
- For further controls ,you may create different user groups like `devops-admins`,`devops-users`,`devops-validators` etc.
- Documentation
    - How to create user groups - https://docs.oracle.com/en-us/iaas/Content/Identity/Tasks/managinggroups.htm#three
    - How to add users to user groups - https://docs.oracle.com/en-us/iaas/Content/devops/using/getting_started.htm#prereq 

</details>

### Dynamic Groups 

<details>
<summary>Devops Pipeline (OCI Repo + Build + Deploy) - Click to expand</summary>

- Create dynamic group (EG: dg-compartname-buildpipeline)for your build pipeline with below rule.

```
ALL {resource.type = 'devopsbuildpipeline', resource.compartment.id = 'compartmentOCID'}

```
- Create dynamic group (EG: dg-compartname-deploymentpipeline)for your deployment pipeline with below rule.

```
All {resource.type = 'devopsdeploypipeline', resource.compartment.id = 'compartmentOCID'}
```

</details>

### Policies

<details>
<summary>OCI Build pipeline - Click to expand</summary>

| Use case | OCI Services  | Statement |
| :---: | :---: | :--- |
| Deliver artifacts  with container registry from Build pipeline | Build pipeline , Container registry | ``` Allow dynamic-group dg-compartname-buildpipeline to manage repos in compartment <compartment_name> ``` |
|Use Vault or Personal Access token (GITHUB/GITLAB etc) with Build piepline |Build pipeline,Vault,Connection|```Allow dynamic-group dg-compartname-buildpipeline to read secret-family in compartment <compartment_name> ```|
|Use OCI Code repo or Invoke deployment from Build pipeline|Build pipeline,Cod repo,Deploy pipeline|```Allow dynamic-group dg-compartname-buildpipeline to manage devops-family in compartment <compartment_name> ```|
|Use Artifact repo with buildpipeline|Buildpipeline,Artifact registry|``` Allow dynamic-group dg-compartname-buildpipeline to manage generic-artifacts in compartment <compartment_name>```|
|Send notifications from buildpipeline|Build pipeline,Notification|```Allow dynamic-group dg-compartname-buildpipeline to use ons-topics in compartment <compartment_name> ```

</details>