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
