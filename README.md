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
<summary>Devops Pipeline (OCI Repo + Build + Deploy) - Click to expand</summary>

| Use case | OCI Services  | Statement |
| :---: | :---: | :---: |
| Deliver artifacts  with container registry | Build pipeline , Container registry | ``` Allow dynamic-group dg-compartname-buildpipeline to manage repos in compartment <compartment_name> ``` |

</details>