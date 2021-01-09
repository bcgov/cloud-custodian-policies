<!--- NOTE: This is a template for your project README. Edit the content according to the comments provided.--->

# AWS SEA Cloud Custodian
<!--- [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](./LICENSE) --->

## Project Status
- [x] Development
- [ ] Production/Maintenance

## Install

```bash
pip install -r requirements.txt
```

## Setup IAM Role

Create `BCGOV_CloudCustodian` IAM role in all accounts with the permissions required to run the policy checks and actions.

## c7n-org: Multi Account Custodian Execution

### Download Script

The script for generating an aws accounts config file is only distributed via git.

```bash
curl https://raw.githubusercontent.com/cloud-custodian/cloud-custodian/master/tools/c7n_org/scripts/orgaccounts.py -o orgaccounts.py
```

### Generate Accounts Config

#### All OUs

```bash
python orgaccounts.py \
    -f accounts.yml \
    --role 'arn:aws:iam::{Id}:role/BCGOV_CloudCustodian' \
```

#### Workload OUs

```bash
python orgaccounts.py \
    -f accounts-workload.yml \
    --role 'arn:aws:iam::{Id}:role/BCGOV_CloudCustodian' \
    --ou Dev --ou Test --ou Prod
```

#### Core OUs

```bash
python orgaccounts.py \
    -f accounts-core.yml \
    --role 'arn:aws:iam::{Id}:role/BCGOV_CloudCustodian' \
    --ou core
```

### Running a Policy with c7n-org

```bash
# Find workload accounts that don't comply with the password policy
c7n-org run -c accounts-workload.yml --dryrun -s output -u policy/common/password.yml --region ca-central-1
```

*Note: `--dryrun` prevents actions from being executed*

## Getting Help or Reporting an Issue
<!--- Example below, modify accordingly --->
To report bugs/issues/feature requests, please file an [issue](../../issues).


## How to Contribute
<!--- Example below, modify accordingly --->
If you would like to contribute, please see our [CONTRIBUTING](./CONTRIBUTING.md) guidelines.

Please note that this project is released with a [Contributor Code of Conduct](./CODE_OF_CONDUCT.md). 
By participating in this project you agree to abide by its terms.


## License
<!--- Example below, modify accordingly --->
    Copyright 2018 Province of British Columbia

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
