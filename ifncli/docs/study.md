# Study commands

## `study:show` Study Show

Show global information about a study
By default output a textual human readable of the json
Arguments:

- `--study_key` key of the study to show
- `--json` output json study definition instead of the textual form
- `--lang` Only output text for this language if provided (default: all)

## `study:list` List studies

Show list of available studies

## `study:list-survey` List surveys in a study

Show list of available survey in a study

Arguments:
- **study_key** : key of the study 
- **--lang** : if provided only show the text for this language (use language code like 'fr', 'en')
- **--json** : Output the full json instead of the textual representation

## `study:show-survey` Show a survey definition

Show a survey definition
By default output a textual human readable of the json

Arguments:

- `--study_key STUDY` key of the study to show
- `--survey SURVEY` key of the survey to show
- `--json` output json study definition instead of the textual form
- `--lang LANG` Only output text for this language if provided (default: all)
- `--format NAME` Output format (see below)
- `--output FILE` Save the generated output in the given file
- `--from-file FILE` Use the survey definition provided in the file, this option doesnt fetch data from the databasae

Output formats:

- human: human readable textual format, it's a yaml-like format but only for reading purpose
- dict-yaml: yaml format (parsable) of the simplified human readable format
- dict-json: json dictionary of the simplified human readable format (use --json to get the full json from API) 
- html: static HTML document of the survey definition

## `study:create` Create a new study

Arguments:

- **--study_def_path**: relative or absolute path the to study definitions folder where config files are placed.

Study definition folder


It has to contain two files:

  1. `props.yaml` with the study properties including study key and secret key, 
  2. `study_rules.json` containing the study rules in a json array.

### Example study props yaml file:
```yaml
studyKey: inf-study-20
secretKey: <add_secret_key_here>
status: active
props:
  systemDefaultStudy: true
  startDate: 1590969600
  name:
    en: Influenzanet 20
    de: Influenzanet 20
  description:
    en: <optional description>
    de: <optional description>
  tags:
    - en: covid-19
      de: covid-19
    - en: flu
      de: flu
```

## `study:manage-members` Manage Study Members

Adding or removing non-admin (RESEARCHER) users for studies:

Arguments:

- **--study_key** : Key of an existing study to which the user should be added to or removed from.

- **--user_id** : ID of the user in the userDB.

- **--user_name** :  Email address of the user or human readable alias.
- **--action** : what action to perform for the given study/user pair. By default ADD, optionally override with REMOVE, to remove a user defined by user_id.

## `study:update-rules` Upload new study rules to an existing study

Upload of new study rules to an existing study

This command will update the study rules with the ones provided by the json file for the study specified by the `survey key`.
The user needs permission to modify the study (study member with OWNER, or MAINTAINER role).

Arguments:

- **--study_key** : Key of an existing study to which the survey should be added or updated in.
- **--rules_json_path** : relative or absolute path to a study rule definition file.

## study:import-survey Update a new survey definition for study

This command will create (if not existing) or update a previous survey definition identified by the `survey key`. If a survey currently exists with the key, by default this will be "unpublished" and the new version published.
The user needs permission to modify the study (study member with OWNER, or MAINTAINER role).

Arguments:

- **--study_key**: Key of an existing study to which the survey should be added or updated in.

- **--survey_json**: relative or absolute path to a survey definition file, e.g., as exported by the study manager app.

### `study:replace-survey` Replace survey object (incl. history)

Before executing the upload, a prompt will ask for confirmation (type "yes" if you want to proceed).

This command will create (if not existing) or update a previous survey definition identified by the `survey key`. 
The user needs permission to modify the study (study member with OWNER, or MAINTAINER role).

Arguments:

- **--study_key** : Key of an existing study to which the survey should be added or updated in.

- **--survey_json** : relative or absolute path to a survey definition file, e.g., as exported by the study manager app.