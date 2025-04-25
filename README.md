# mapp_documentation

### ORG_POC_SURVEY_LIST
Changed from this
```
export const ORG_POC_SURVEY_LIST =gql`
  query allOrgSurveysByImplicitOrgId{
    allOrgSurveysByImplicitOrgId(listing:true){
        edges{
            node{
                id
                name
                 multisourceResponse
            }
        }
    }
  }
`
```
to this
```
export const ORG_POC_SURVEY_LIST =gql`
  query allOrgSurveysByImplicitOrgId($orgId: Int){
    orgSurveysByOrgId(listing:true, orgId: $orgId){
        edges{
            node{
          id
          name
          multisourceResponse
        }
      }
    }
  }
`
```
#### Places Changed
+ src/modules/poc-dashboard/containers/dashboard/PocDashboardHomeContainer.jsx --> getOrgSurveyList
+ src/modules/poc-dashboard/containers/dashboard/surveyResponseVerticalContainer.jsx --> getOrgSurveyList

### ORG_EMPLOYEE_LEVEL_COUNTS #Doubt
Changed from this
```
export const ORG_MANAGER_EMPLOYEE_COUNT = gql`
  query me {
    me {
     id
     employee{
        id
        teamManagerEmployee{
            totalCount
        }
        orgCeoEmployee{
            totalCount
        }
        orgPocEmployee{
            totalCount
        }
        verticalHeadEmployee{
            totalCount
        }
     }
    }
  }
`;
```
to this
```
export const ORG_MANAGER_EMPLOYEE_COUNT = gql`
query me {
  me {
    id
    employee{
      id
      teamManagerEmployee{
        totalCount
      }
      orgAmEmployee{
        totalCount
      }
      orgCeoEmployee{
        totalCount
      }
      orgPocEmployee{
        totalCount
      }
      verticalHeadEmployee{
        totalCount
      }
     }
    }
  }
`;
```
#### Places Changed
+ /Users/dnyaneshwar/Work/front-end/mapp-ui/src/modules/poc-dashboard/containers/dashboard/assessmentReportContainer.jsx --> getEmployeeData()
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  -->

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  -->

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 

### ORG_POC_SURVEY_LIST
Changed from this
```

```
to this
```

```
#### Places Changed
+  --> 
+  --> 
