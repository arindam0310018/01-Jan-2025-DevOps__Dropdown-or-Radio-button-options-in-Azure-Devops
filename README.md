# Dropdown or Radio button options in Azure Devops:-

Greetings to my fellow Technology Advocates and Specialists.

In this Session, I will demonstrate __Dropdown OR Radio button options in Azure Devops.__

| __AUTOMATION OBJECTIVES:-__ |
| --------- |

| __#__ | __TOPICS__ |
| --------- | --------- |
| 1. | Radio Button option as Runtime Variables in Azure Devops Pipelines. |
| 2. | Dropdown Menu option as Runtime Variables in Azure Devops Pipelines. |
| 3. | Spot the difference. |

| IMPORTANT NOTE:- |
| --------- |

The YAML Pipeline is tested on __WINDOWS BUILD AGENT__ Only!!!

| __REQUIREMENTS:-__ |
| --------- |

1. Azure Subscription.
2. Azure DevOps Organisation and Project.
3. Service Principal with Required RBAC ( Contributor) applied on Subscription or Resource Group(s).
4. Azure Resource Manager Service Connection in Azure DevOps.

| HOW DOES MY CODE PLACEHOLDER LOOKS LIKE:- |
| --------- |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/d11e7ckkyjuii2r4xi2t.jpg) |

| __1. RADIO BUTTON OPTION AS RUNTIME VARIABLES:-__ |
| --------- |

| PIPELINE CODE SNIPPET:- | 
| --------- |

| AZURE DEVOPS YAML PIPELINE (azure-pipelines-runtime-parameter-options-v1.0.yml):- |
| --------- |

```
trigger:
  none

##################
# Radio Button:-
##################
parameters:
  - name: environment
    displayName: Select environment
    type: string
    default: 'dev'
    values:
      - dev
      - test
      - uat

#############
#Variables:-
############
variables:
  ServiceConnection: 'amcloud-cicd-service-connection' # Please replace with your Service Connection!
  BuildAgent: 'windows-latest' # Please replace with your Build Agent. You can continue to use this as this is Microsoft Hosted Windows Build Agent!

######################
# Declare Build Agent:-
######################
pool:
  vmImage: '$(BuildAgent)'

##################################
# Declare Stages:-
# Test Runtime parameters as:-
# 1. Radio Button
##################################
stages:
- stage: Test_Runtime_Parameters_RadioButton
  displayName: Test Runtime Parameters Radio Button
  jobs:
  - job: Test_Runtime_Parameters_RadioButton
    steps:
    - task: AzureCLI@2
      displayName: Test Runtime Parameters RadioButton
      inputs:
        azureSubscription: '$(ServiceConnection)'
        scriptLocation: 'inlineScript'
        scriptType: 'ps'
        inlineScript: |
          echo "Deploying to ${{ parameters.environment }} environment"
```

| __CODE BLOCK FOR RADIO BUTTON AS RUNTIME VARIABLES IN YAML:-__ |
| --------- |

```
##################
# Radio Button:-
##################
parameters:
  - name: environment
    displayName: Select environment
    type: string
    default: 'dev'
    values:
      - dev
      - test
      - uat
```

| __OUTPUT: RADIO BUTTON OPTION AS RUNTIME VARIABLES__ | 
| --------- |
| 1. Radio Button as runtime variables is displayed successfully on Pipeline Execution. |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/g613mz3u1178uj1dvjgb.jpg) |
| 2. Successful Pipeline Execution. |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nddjllxwtrs1x3sss4hi.jpg) |

| __2. DROPDOWN MENU OPTION AS RUNTIME VARIABLES:-__ |
| --------- |

| PIPELINE CODE SNIPPET:- | 
| --------- |

| AZURE DEVOPS YAML PIPELINE (azure-pipelines-runtime-parameter-options-v1.1.yml):- |
| --------- |

```
trigger:
  none

##################
# Drop Down Menu:-
##################
parameters:
  - name: environment
    displayName: Select environment
    type: string
    default: 'dev'
    values:
      - dev
      - test
      - uat
      - prod

#############
#Variables:-
############
variables:
  ServiceConnection: 'amcloud-cicd-service-connection' # Please replace with your Service Connection!
  BuildAgent: 'windows-latest' # Please replace with your Build Agent. You can continue to use this as this is Microsoft Hosted Windows Build Agent!

######################
# Declare Build Agent:-
######################
pool:
  vmImage: '$(BuildAgent)'

##################################
# Declare Stages:-
# Test Runtime parameters as:-
# 1. Dropdown Menu
##################################
stages:
- stage: Test_Runtime_Parameters_DropDown_Menu
  displayName: Test Runtime Parameters Dropdown Menu
  jobs:
  - job: Test_Runtime_Parameters_DropDown_Menu
    steps:
    - task: AzureCLI@2
      displayName: Test Runtime Parameters Dropdown Menu
      inputs:
        azureSubscription: '$(ServiceConnection)'
        scriptLocation: 'inlineScript'
        scriptType: 'ps'
        inlineScript: |
          echo "Deploying to ${{ parameters.environment }} environment"
```

| __CODE BLOCK FOR DROPDOWN MENU AS RUNTIME VARIABLES IN YAML:-__ |
| --------- |

```
##################
# Drop Down Menu:-
##################
parameters:
  - name: environment
    displayName: Select environment
    type: string
    default: 'dev'
    values:
      - dev
      - test
      - uat
      - prod
```

| __OUTPUT: DROPDOWN MENU OPTION AS RUNTIME VARIABLES__ | 
| --------- |
| 1. Dropdown Menu as runtime variables is displayed successfully on Pipeline Execution. |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wf71d0drqy97vgnzr8bk.jpg) |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rqskv6u9cz2bcc10oz5k.jpg) |
| 2. Successful Pipeline Execution. |
| ![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wtqo1w98ghgmeqi4cgop.jpg) |

| __3. SPOT THE DIFFERENCE:-__ |
| --------- |
| The __"type"__ of the variable is exactly the same except the no. of values. For __"Radio button"__, we entered 3 values but if we needed __"Dropdown Menu"__, we just increased 1 more value. __"Radio button"__ option changes to __"Dropdown Menu"__. |
| For __"Radio button"__, value count <= 3 |
| For __"Dropdown Menu"__, value count > 3 |

__Hope You Enjoyed the Session!!!__

__Stay Safe | Keep Learning | Spread Knowledge__
