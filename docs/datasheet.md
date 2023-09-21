# Overview

## Basics: contact, distribution, access

### 1. Dataset name
GitHub Innovation Graph Metrics

### 2. Dataset version number and date
Last updated: 2023-09-21

Version: 1.0.0

### 3. Dataset owner/manager contact information, including name and email
The GitHub Policy Team manages the dataset. Inquiries can be made to policy@github.com. Please use a subject line that includes “GitHub Innovation Graph.”

### 4. Who can access this dataset?
The dataset is openly accessible.

### 5. How can the dataset be accessed?
The dataset can be accessed at its dedicated repository: github.com/github/innovationgraph

## Dataset contents

### 6. What are the contents of this dataset? 
The dataset is composed of 8 CSV files of GitHub metrics, aggregated by economy and reported quarterly. Each metric is reported quarterly dating back to January 2020. Metrics for economies are only reported when there are 100 or more unique developers performing the relevant activity within the time period.

Metrics of activity are assigned to a location based on the relevant user as determined by their IP address when interacting with GitHub. If a user changes locations in the time period, the location for all user-relevant activity would be determined by the mode of location sampled daily in the period. Concretely, if a developer were contributing to open source projects in the United States for two months, but also made contributions while traveling in India, all activity from that developer during that quarter would be assigned to the United States.

Additionally, the last known location of the developer is carried forward on a daily basis even if no activities were performed by the developer that day. For example, if a developer performed activities within the United States and then became inactive for 6 days, that developer would be considered to be in the United States for that 7-day span.

We report on the following metrics:

1. **Git pushes**: the number of times developers in a given economy uploaded code to GitHub. See the [documentation for `git push`](https://git-scm.com/docs/git-push) for a description of the `git push` command. [Changes to files made through GitHub’s online platform](https://docs.github.com/repositories/working-with-files/managing-files/editing-files) automatically result in a push. Note that a single git push may contain multiple commits.
2. **Repositories**: the number of software projects in a given economy based on the mode location of all repository members with triage and above access. See our [documentation for Repositories](https://docs.github.com/repositories) for more information.
3. **Developers**: the number of developer accounts located in a given economy based on mode daily location. This count excludes users that are bots or otherwise flagged as “spammy” within internal systems. See our [documentation for personal accounts](https://docs.github.com/get-started/learning-about-github/types-of-github-accounts#personal-accounts) for more information.
4. **Organizations**: the number of developer groups in a given economy, including companies, academic groups, nonprofits, and informal collectives that organize activity on GitHub. Location is assigned based on the mode location of all organization members. See our [documentation for Organizations](https://docs.github.com/organizations) for more information.
5. **Programming languages**: the number of unique developers in each economy who made at least one git push to a repository with a given programming language. See our [documentation for repository languages](https://docs.github.com/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-repository-languages) for more information about how we detect programming languages.
6. **Licenses**. the number of unique developers in each economy who made at least one git push to a repository with a given license. See our [documentation for Licenses](https://docs.github.com/rest/licenses/licenses) for more information about how we classify repositories by license. Note that [`NOASSERTION`](https://spdx.github.io/spdx-spec/v2.3/package-information/#713-concluded-license-field) in the data or `Other` (displayed) means a license file was found but could not be identified with high confidence, or multiple licenses were present in a repository.
7. **Topics**: the number of unique developers who made at least one git push to a repository with a given topic. See our [documentation for Topics](https://docs.github.com/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/classifying-your-repository-with-topics) for more information about how developers assign topics to repositories.
8. **Economy collaborators**: the volume of collaboration on software projects based on the sum of git pushes sent and pull requests opened by a developer to a repository owned by another developer or organization. See the [documentation for `git push`](https://git-scm.com/docs/git-push) for a description of the `git push` command. See our documentation for [Pull Requests](https://docs.github.com/pull-requests) and [Repositories](https://docs.github.com/repositories) for more information about supported functionality.

#### CSV file schemas

##### Schema for `git_pushes.csv`

| git_pushes | iso2_code | year | quarter |
| --- | --- | --- | --- |
| integer | string | integer | integer |

##### Schema for `repositories.csv`

| repositories | iso2_code | year | quarter |
| --- | --- | --- | --- |
| integer | string | integer | integer |
##### Schema for `developers.csv`

| developers | iso2_code | year | quarter |
| --- | --- | --- | --- |
| integer | string | integer | integer |
##### Schema for `organizations.csv`

| organizations | iso2_code | year | quarter |
| --- | --- | --- | --- |
| integer | string | integer | integer |
##### Schema for `languages.csv`

| num_pushers | language | language_type | iso2_code | year | quarter
| --- | --- | --- | --- | --- | --- |
| integer | string | string | string | integer | integer |

##### Schema for `licenses.csv`

| num_pushers | spdx_license | iso2_code | year | quarter
| --- | --- | --- | --- | --- |
| integer | string | string | integer | integer |

##### Schema for `topics.csv`

| num_pushers | topic | iso2_code | year | quarter
| --- | --- | --- | --- | --- |
| integer | string | string | integer | integer |

##### Schema for `economy_collaborators.csv`

| weight | source | destination | iso2_code | year | quarter
| --- | --- | --- | --- | --- | --- |
| integer | string | string | string | integer | integer |
## Intended & inappropriate uses

### 7. What are the intended purposes for this dataset?
Innovation Graph metrics are intended to support research and public policy that could benefit from data on software development activity globally. We welcome developers to explore the data, discover insights, and create visualizations, among much more.

### 8. What are some tasks/purposes that this dataset is not appropriate for?
Innovation Graph metrics are not appropriate for understanding individual projects or individual developers’ activity. The dataset is unlikely to be of use for training specific purpose machine learning systems. It is not intended to replace API queries for specific data needs. 

# Details

## Data collection procedures

### 9. How was the data collected?
Data is collected in the course of regular developer activity on, and operation of, the GitHub platform. GitHub staff use the data to construct the Innovation Graph metrics.

As described further in the Data Quality section below, we excluded activity from users that were deemed to be automated or inauthentic, and filtered terms that might individually identify users, such as in the case of the Topics metric.

### 10. Considerations taken for responsible and ethical data collection
As guided by the GitHub Privacy Statement, we have used platform data to conduct this research. We aggregate individual-level activity and use a reporting threshold of 100 unique developers performing an activity within the time period. If this threshold is not met, we do not report the metric for that economy. The intent is to minimize any privacy risk to individuals. The raw data underlying the public metrics was accessible to only select GitHub employees in the preparation of the data set, and then only under appropriate controls.

## Representativeness

### 11. How representative is this dataset? What population(s), contexts (e.g., scripted vs. conversational speech), conditions (e.g., lighting for images) is it representative of?
Innovation Graph metrics reflect developer activity on GitHub. Although these offer valuable insights into software development, GitHub data alone paints an incomplete picture; we are but one resource in the ecosystem. 

### 12. What demographic groups (e.g., gender, race, age, etc.) are identified in the dataset, if any?
No demographic groups are identified in this dataset.

## Data quality

### 13. Is there any missing information in the dataset? If yes, please explain what information is missing and why (e.g., some people did not report their gender).
Metrics for economies are only reported when there are 100 or more unique developers performing the relevant activity within the time period. This means that economies with small numbers of GitHub developers will be missing. As such, Innovation Graph metrics are not useful for understanding software development in these smaller economies.

Additionally, we excluded developers whose activity volume exceeded a threshold that could be reasonably attributed to human activity and developers who were classified by our automated systems as inauthentic. Thus, Innovation Graph metrics are not useful for understanding the adoption and behavior of bots on GitHub.

We assign the location of repositories and organizations based on the mode location of the members. For the economy collaborator metric, which relies on these locations, this may in effect under-count cross-border collaboration where contributions to a repo may affect users collaborating from many economies, not simply one as calculated in our metric. As such, economy collaborators should be viewed as a lower bar as opposed to a precise measure.

For metrics related to repositories, we only report on numbers and activity related to those that are public. As a result, Innovation Graph metrics are not useful for understanding the volume and activity of software development in private repositories.

### 14. What errors, sources of noise, or redundancies are important for dataset users to be aware of?
GitHub activity is assigned to an economy based on the IP address of the given developer or organization. Thus, VPNs and other means of altering or hiding IP addresses distort the metrics. Economies where developers may be more likely to use such tools will be affected more than others; thus, international comparisons should note this limitation.

### 15. How was the data validated/verified? 
GitHub staff manually verified samples of the results for each data query.

## Additional details on distribution & access

### 16. How can dataset users receive information if this dataset is updated (e.g., corrections, additions, removals)?
If you use this dataset for your research, please watch the GitHub Innovation Graph repository to subscribe to changes.

### 17. What will happen to older versions of the dataset? Will they continue to be maintained?
The dataset will be updated quarterly, with previous files deleted but their contents carried over to the new files. Of course, the previous versions will be available in the git history of this repository.

### 18. Describe any applicable intellectual property (IP) licenses, copyright, fees, terms of use, export controls, or other regulatory restrictions that apply to this dataset or individual data points. 
The dataset is made available under a CC0-1.0 license.
