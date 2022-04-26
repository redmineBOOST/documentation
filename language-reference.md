---
layout: documentation
title: Reference
id: reference
---
# Language Reference (2022-04-26)

The modifiers have the following meanings:

***`readonly`*** : A read-only property is not writable and can only be accessed. That is, when a Redmine item is queried or instantiated as an item, read-only properties cannot be set.

***`required`*** : A required property must be set in instantiable items.

## <a name='type-category-enumeration'></a> Enumerations


### <a name='type-echomode'></a> `EchoMode`


This enum is used in input items and controls whether the typed characters are printed or are hidden by stars.

#### Fields

| Name | Value | Description |
|:-|:-|:-|
|`Normal`|`0`|Show characters as user types them|
|`Password`|`1`|Show characters as user types them|

### <a name='type-issuestatusfilter'></a> `IssueStatusFilter`


[Issues](#type-issue) can be open or closed. This enum represents the filter for the state.

#### Fields

| Name | Value | Description |
|:-|:-|:-|
|`All`|`0`|The status of an issue does not matter|
|`Closed`|`1`|Show only closed issues|
|`Open`|`2`|Show only opened issues|

### <a name='type-permission'></a> `Permission`


Permissions are contained in roles and control whether a [User](#type-user) or [Group](#type-group) has the right to perform an action or not.

#### Fields

| Name | Value | Description |
|:-|:-|:-|
|`AddIssueNotes`|`1`|	Allowed to add notes to issues|
|`AddIssues`|`2`|Allowed to add issues|
|`AddProjects`|`3`|Allowed to add projects|
|`DeleteIssues`|`4`|Allowed to delete issues|
|`DeleteProjects`|`5`|Allowed to delete projects|
|`EditIssues`|`6`|Allowed to edit issues|
|`EditOwnIssues`|`7`|Allowed to edit own issues|
|`EditProjects`|`8`|Allowed to edit projects|
|`ManageIssueRelations`|`9`|Allowed to edit issue relations issues|
|`ManageMembers`|`10`|Allowed to edit project members|
|`ManageSubtasks`|`11`|Allowed to edit subtasks|
|`SelectProjectModules`|`12`|Allowed to select project modules|
|`SetIssuesPrivate`|`13`|Allowed to set issues private state|
|`SetOwnIssuesPrivate`|`14`|Allowed to set own issues private state|
|`Unknown`|`0`|Database default value but should never happen|

### <a name='type-projectmodule'></a> `ProjectModule`


Contained in each [Project](#type-project).

#### Fields

| Name | Value | Description |
|:-|:-|:-|
|`Boards`|`0`|Boards Module|
|`Calendar`|`1`|Calendar Module|
|`Documents`|`2`|Documents Module|
|`Files`|`3`|Files Module|
|`Gantt`|`4`|Gantt Module|
|`IssueTracking`|`5`|Issue Tracking Module|
|`News`|`6`|News Module|
|`Repository`|`7`|Repository Module|
|`TimeTracking`|`8`|Time Tracking Module|
|`Wiki`|`9`|Wiki Module|

### <a name='type-userstatus'></a> `UserStatus`


Contained in each [User](#type-user).

#### Fields

| Name | Value | Description |
|:-|:-|:-|
|`Active`|`1`|[User](#type-user) can login and use their account|
|`Anonymous`|`0`|Database default value but should never happen|
|`Locked`|`3`|[User](#type-user) was once active and is now locked, [User](#type-user) can not login|
|`Registered`|`2`|[User](#type-user) has registered but not yet confirmed their email address or was not yet activated by an administrator, User can not login|

## <a name='type-category-inputitem'></a> Input Items

Input Items provide an interface for user input.

All IO Items have a dedicated readonly `value` property which contains the result after the item was executed.


### <a name='type-choice`1'></a> Choice<T>


A [Choice](#type-choice) is an input item which renders as a list and the user can choose an element from it.

The generic parameter `T` modifies the element type of the `options` array and is the returning type of the `value` property.

The user can navigate with the `UP` or `DOWN` arrows and to continue press the `ENTER` key.


**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`description`|[`string`](#type-string) <code>&#124;</code> `undefined`||Description text which is shown when rendering the input|
|`options`|`[`[`T`](#type-t)`]`|required|Choosable options|
|`searchable`|[`bool`](#type-bool)||Adds a searchbar, defaults to false|
|`value`|[`T`](#type-t)|readonly|Selected element|

### <a name='type-dateinput'></a> DateInput


A [DateInput](#type-dateinput) is an input item which renders a text input where the user can specify a date.

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`description`|[`string`](#type-string) <code>&#124;</code> `undefined`||Description text which is shown when rendering the input|
|`format`|[`string`](#type-string) <code>&#124;</code> `undefined`||Format overrides locale, for details about valid formatting codes see [Standard Date and Time Format Strings](https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-date-and-time-format-strings) or [Custom Date and time Format Strings](https://docs.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings)|
|`locale`|[`string`](#type-string) <code>&#124;</code> `undefined`||When no format or locale is given, the OS locale is used, culture names follow the standard defined by [BCP 47](https://www.rfc-editor.org/info/bcp47), for a list of predefined culture names see the **Language tag** column in the [list of language/region names](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)|
|`value`|[`date`](#type-date)|readonly|Specified date|

### <a name='type-lineinput'></a> LineInput


A [LineInput](#type-lineinput) is an input item which renders a text input where the user can specify a text.

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`description`|[`string`](#type-string) <code>&#124;</code> `undefined`||Description text which is shown when rendering the input|
|`echoMode`|[`EchoMode`](#type-echomode)||Echo mode of the input, defaults to *[EchoMode](#type-echomode).Normal*|
|`maxLength`|[`int32`](#type-int32) <code>&#124;</code> `undefined`||Maximum length of the input text|
|`minLength`|[`int32`](#type-int32) <code>&#124;</code> `undefined`||Minimum length of the input text|
|`pattern`|[`string`](#type-string) <code>&#124;</code> `undefined`||Validation pattern of the input text (see [Regular Expressions](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference)), the `$` sign has to be **escaped** with the `` ` ``|
|`value`|[`string`](#type-string)|readonly|Specified text|

### <a name='type-multichoice`1'></a> MultiChoice<T>


A [MultiChoice](#type-multichoice) is an input item which renders as a list and the user can choose multiple elements from it.

The generic parameter `T` modifies the element type of the `options` and `values` array.

The user can navigate with the `UP` or `DOWN` arrows.
To select elements in a [MultiChoice](#type-multichoice) the user can press the `SPACE` and to continue the `ENTER` key.

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`description`|[`string`](#type-string) <code>&#124;</code> `undefined`||Description text which is shown when rendering the input|
|`options`|`[`[`T`](#type-t)`]`|required|Choosable options|
|`searchable`|[`bool`](#type-bool)||Adds a searchbar, defaults to *false*|
|`values`|`[`[`T`](#type-t)`]`|readonly|Selected elements|

### <a name='type-textinput'></a> TextInput


A [TextInput](#type-textinput) is a Multi-Line input item which opens the external text editor with a temporary file and after the file is
saved and the editor closed it will continue with the process execution.

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`description`|[`string`](#type-string) <code>&#124;</code> `undefined`||Description text which is shown when rendering the input|
|`value`|[`string`](#type-string)|readonly|Text that was input by the user|


## <a name='type-category-redmineitem'></a> Redmine Items


### <a name='type-attachment'></a> Attachment


When an [Upload](#type-upload) item has been executed, it is transformed into an [Attachment](#type-attachment).
Attachments can be retrieved from an [Issue](#type-issue).

**Instantiable:** no

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`author`|[`User`](#type-user)|readonly|[User](#type-user) which uploaded the [Attachment](#type-attachment)|
|`content_type`|[`string`](#type-string) <code>&#124;</code> `undefined`|readonly|MIME-Typ can be null if it is unknown|
|`content_url`|[`string`](#type-string)|readonly|[Attachment](#type-attachment) URL|
|`created_on`|[`date`](#type-date)|readonly|date when it was created|
|`description`|[`string`](#type-string) <code>&#124;</code> `undefined`|readonly|Description of the [Attachment](#type-attachment)|
|`filename`|[`string`](#type-string)|readonly|Filename of the [Attachment](#type-attachment)|
|`filesize`|[`int32`](#type-int32)|readonly|Filesize of the [Attachment](#type-attachment) in Bytes|

### <a name='type-authentication'></a> Authentication


The [Authentication](#type-authentication) item contains all password related options for an user.

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`generatePassword`|[`bool`](#type-bool)||Either `generatePassword` or `password` must be set. If defined, `password` can not be defined|
|`mustChangePassword`|[`bool`](#type-bool)||[User](#type-user) has to change the password after login|
|`password`|[`string`](#type-string)||Either `generatePassword` or `password` must be set. If defined, `generatePassword` can not be defined|
|`sendInformation`|[`bool`](#type-bool)||Send acocunt information to the user via mail|

### <a name='type-blockedby'></a> BlockedBy


Creates a [BlockedBy](#type-blockedby) issue relation.
The [BlockedBy](#type-blockedby) item is an issue relation where the containing issue is blocked by the issue specified in the property.
Other relations are [Follows](#type-follows) and [RelatedTo](#type-relatedto).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`issue`|[`Issue`](#type-issue)|required|[Issue](#type-issue) which blocks the containing issue|

### <a name='type-follows'></a> Follows


Creates a [Follows](#type-follows) issue relation.
The [Follows](#type-follows) item is an issue relation where the containing issue is following the issue specified in the property.
Other relations are [BlockedBy](#type-blockedby) and [RelatedTo](#type-relatedto).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`issue`|[`Issue`](#type-issue)|required|[Issue](#type-issue) which precedes the containing issue|
|`delay`|[`int32`](#type-int32) <code>&#124;</code> `undefined`||Delay in days|

### <a name='type-group'></a> Group


Creates a Redmine [Group](#type-group).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`memberships`|`[`[`Membership`](#type-membership)`]`|readonly|Memberships of the [Group](#type-group)|
|`name`|[`string`](#type-string)|required|Name of the [Group](#ype-group)|
|`users`|`[`[`User`](#type-user)`]` <code>&#124;</code> `restricted`||Users of the [Group](#type-group)|

### <a name='type-issue'></a> Issue


Creates a Redmine [Issue](#type-issue).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)
* [`BlockedBy`](#type-blockedby)
* [`Follows`](#type-follows)
* [`Issue`](#type-issue)
* [`Note`](#type-note)
* [`RelatedTo`](#type-relatedto)
* [`Upload`](#type-upload)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`assignedTo`|[`Group`](#type-group) <code>&#124;</code> [`User`](#type-user) <code>&#124;</code> `undefined`||Assignee of the [Issue](#type-issue)|
|`attachments`|`[`[`Attachment`](#type-attachment)`]`|readonly|Attachments of the [Issue](#type-issue)|
|`author`|[`User`](#type-user)|readonly|Author of the [Issue](#type-issue)|
|`category`|[`IssueCategory`](#type-issuecategory) <code>&#124;</code> `undefined`||Category of the [Issue](#type-issue)|
|`children`|`[`[`Issue`](#type-issue)`]`|readonly|Direct Child Issues of the [Issue](#type-issue)|
|`closedOn`|[`date`](#type-date) <code>&#124;</code> `undefined`|readonly|Closed date of the [Issue](#type-issue)|
|`createdOn`|[`date`](#type-date)|readonly|Created date of the [Issue](#type-issue)|
|`description`|[`string`](#type-string) <code>&#124;</code> `undefined`||Description of the [Issue](#type-issue)|
|`doneRatio`|[`int32`](#type-int32)||Defaults to *zero*, only settable if no child issues exist|
|`dueDate`|[`date`](#type-date) <code>&#124;</code> `undefined`||Only settable if no child issues exist|
|`estimatedHours`|[`float32`](#type-float32) <code>&#124;</code> `undefined`||Estimated hours of the [Issue](#type-issue)|
|`isPrivate`|[`bool`](#type-bool)||Private State of the [Issue](#type-issue)|
|`parent`|[`Issue`](#type-issue) <code>&#124;</code> `undefined`||Parent of the [Issue](#type-issue), is set automatically if the [Issue](#type-issue) is nested|
|`priority`|[`IssuePriority`](#type-issuepriority)||Defaults to default priority, only settable if no child issues exist|
|`project`|[`Project`](#type-project)|required|[Project](#type-project) of the [Issue](#type-issue)|
|`relations`|[`BlockedBy`](#type-blockedby) <code>&#124;</code> [`Follows`](#type-follows) <code>&#124;</code> [`RelatedTo`](#type-relatedto)|readonly|Relations of the [Issue](#type-issue)|
|`spentHours`|[`float32`](#type-float32)|readonly|Spent hours of the [Issue](#type-issue)|
|`startDate`|[`date`](#type-date)||Only settable if no child issues exist|
|`status`|[`IssueStatus`](#type-issuestatus)||Defaults to default status in tracker|
|`subject`|[`string`](#type-string)|required|Subject of the [Issue](#type-issue)|
|`totalEstimatedHours`|[`float32`](#type-float32) <code>&#124;</code> `undefined`|readonly|Total estimated hours of the [Issue](#type-issue)|
|`totalSpentHours`|[`float32`](#type-float32)|readonly|Total spent hours of the [Issue](#type-issue), defaults to *zero*|
|`tracker`|[`Tracker`](#type-tracker)|required|[Tracker](#type-tracker) of the [Issue](#type-issue)|
|`updatedOn`|[`date`](#type-date)|readonly|Updated date of the [Issue](#type-issue)|

### <a name='type-issuecategory'></a> IssueCategory


Issue Categories can be retrieved from an [Project](#type-project).

**Instantiable:** no

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`name`|[`string`](#type-string)|required|Name of the [IssueCategory](#type-issuecategory)|

### <a name='type-issuepriority'></a> IssuePriority


Issue Priorities can be retrieved from queries e. g. with [GetIssuePriorities()](#query-getissuepriorities).

**Instantiable:** no

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`active`|[`bool`](#type-bool)||Active state of the [IssuePriority](#type-issuepriority)|
|`isDefault`|[`bool`](#type-bool)||Is default state of the [IssuePriority](#type-issuepriority)|
|`name`|[`string`](#type-string)|required|Name of the [IssuePriority](#type-issuepriority)|

### <a name='type-issuestatus'></a> IssueStatus


An [IssueStatus](#type-issuestatus) is the state if an issue is closed or not.

Issue Statuses can be retrieved from queries e.g. with [GetIssueStatuses()](#query-getissuestatuses) or the [Issue](#type-issue).

**Instantiable:** no

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`isClosed`|[`bool`](#type-bool)||Is closed state of the [IssueStatus](#type-issuestatus)|
|`name`|[`string`](#type-string)|required|Name of the [IssueStatus](#type-issuestatus)|

### <a name='type-membership'></a> Membership


Memberships include users of a project and their roles.

Memberships can be retrieved from a [User](#type-user), [Group](#type-group) and even a [Project](#type-project).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`assignee`|[`Group`](#type-group) <code>&#124;</code> [`User`](#type-user)|required|Assignee of the [Membership](#type-membership)|
|`project`|[`Project`](#type-project)|required|[Project](#type-project) of the [Membership](#type-membership), is set automatically if the [Membership](#type-membership) is nested|
|`roles`|`[`[`Role`](#type-role)`]`|required|Roles of the [Membership](#type-membership)|

### <a name='type-note'></a> Note


Appends a [Note](#type-note) to the containing [Issue](#type-issue).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`isPrivate`|[`bool`](#type-bool)||Is private state of the [Note](#type-note)|
|`text`|[`string`](#type-string)|required|Text of the [Note](#type-note)|

### <a name='type-project'></a> Project


Represents a Redmine [Project](#type-project).

Projects can be retrieved e.g. with queries like [GetProjects()](#query-getprojects).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)
* [`Membership`](#type-membership)
* [`Project`](#type-project)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`createdOn`|[`date`](#type-date)|readonly|Creation date of the [Project](#type-project)|
|`customModules`|`[`[`string`](#type-string)`]`||Custom modules of the [Project](#type-project)|
|`description`|[`string`](#type-string) <code>&#124;</code> `undefined`||Description of the [Project](#type-project)|
|`identifier`|[`string`](#type-string)|required|Identifier of the [Project](#type-project)|
|`inheritMembers`|[`bool`](#type-bool)||Flag if the [Project](#type-project) should inherit members|
|`isPublic`|[`bool`](#type-bool)||Is public state of the [Project](#type-project)|
|`issueCategories`|`[`[`IssueCategory`](#type-issuecategory)`]`|readonly|[Issue](#type-issue) categories of the [Project](#type-project)|
|`memberships`|`[`[`Membership`](#type-membership)`]`|readonly|Memberships of the [Project](#type-project)|
|`name`|[`string`](#type-string)|required|Name of the [Project](#type-project)|
|`parent`|[`Project`](#type-project) <code>&#124;</code> `undefined`||Parent of the [Project](#type-project), is set automatically if the [Project](#type-project) is nested|
|`standardModules`|`[`[`ProjectModule`](#type-projectmodule)`]`||[Modules](#type-projectmodule) of the [Project](#type-project)|
|`trackers`|`[`[`Tracker`](#type-tracker)`]`|readonly|[Tracker](#type-tracker) of the [Project](#type-project)|
|`updatedOn`|[`date`](#type-date) <code>&#124;</code> `undefined`|readonly|Update date of the [Project](#type-project)|

### <a name='type-relatedto'></a> RelatedTo


The [RelatedTo](#type-relatedto) item is an issue relation where the containing issue is related to the issue specified in the property.
Other relations are [BlockedBy](#type-blockedby) and [Follows](#type-follows).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`issue`|[`Issue`](#type-issue)|required|[Issue](#type.issue) which relates to the containing issue|

### <a name='type-removeattachments'></a> RemoveAttachments


Removes a set of [Attachments](#type-attachment).

**Instantiable:** yes

**Minimum Redmine Version:** 3.3.0

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`attachments`|`[`[`Attachment`](#type-attachment)`]`||[Attachments](#type-attachment) which shall be deleted|

### <a name='type-removeissues'></a> RemoveIssues


Remove [Issues](#type-issue) from a [Project](#type-project)

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`issues`|`[`[`Issue`](#type-issue)`]`||[Issues](#type-issue) to remove|

### <a name='type-removememberships'></a> RemoveMemberships


Remove [Memberships](#type-membership)

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`memberships`|`[`[`Membership`](#type-membership)`]`||[Memberships](#type-membership) to remove|

### <a name='type-removeprojects'></a> RemoveProjects


Remove [Projects](#type-project)

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`projects`|`[`[`Project`](#type-project)`]`||[Projects](#type-project) to remove|

### <a name='type-removerelations'></a> RemoveRelations


Removes a set of isssue relations e.g. [BlockedBy](#type-blockedby), [Follows](#type-follows) or [RelatedTo](#type-relatedto).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`relations`|`[`[`BlockedBy`](#type-blockedby) <code>&#124;</code> [`Follows`](#type-follows) <code>&#124;</code> [`RelatedTo`](#type-relatedto)`]`|required|Relations which should be deleted|

### <a name='type-role'></a> Role


A [Role](#type-role) a [User](#type-user) can have on a [Project](#type-project).

**Instantiable:** no

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`assignable`|[`bool`](#type-bool)||Assignable state of the [Role](#type-role)|
|`name`|[`string`](#type-string)|required|Name of the [Role](#type-role)|
|`permissions`|`[`[`Permission`](#type-permission)`]`||Permissions of the [Role](#type-role)|

### <a name='type-tracker'></a> Tracker


Represents a Redmine [Tracker](#type-tracker).

**Instantiable:** no

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`defaultStatus`|[`IssueStatus`](#type-issuestatus)|required|Default [IssueStatus](#type-issuestatus) of the [Tracker](#type-tracker)|
|`description`|[`string`](#type-string)||Description of the [Tracker](#type-tracker)|
|`name`|[`string`](#type-string)|required|Name of the [Tracker](#type-tracker)|

### <a name='type-updategroup'></a> UpdateGroup


Updates an existing [Group](#type-group).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`addUsers`|`[`[`User`](#type-user)`]`||Users to be added to the [Group](#type-group), can not be set if 'users' is set|
|`group`|[`Group`](#type-group)|required|[Group](#type-group) to update|
|`name`|[`string`](#type-string)||Name of the [Group](#type-group)|
|`removeUsers`|`[`[`User`](#type-user)`]`||Users to be removed from the [Group](#type-group), can not be set if 'users' is set|
|`users`|`[`[`User`](#type-user)`]`||Users of the [Group](#type-group), can not be set if 'addUsers' or 'removeUsers' is set|

### <a name='type-updateissue'></a> UpdateIssue


Updates an existing [Issue](#type-issue).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)
* [`BlockedBy`](#type-blockedby)
* [`Follows`](#type-follows)
* [`Issue`](#type-issue)
* [`Note`](#type-note)
* [`RelatedTo`](#type-relatedto)
* [`Upload`](#type-upload)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`assignedTo`|[`Group`](#type-group) <code>&#124;</code> [`User`](#type-user) <code>&#124;</code> `undefined`||Assignee of the [Issue](#type-issue)|
|`category`|[`IssueCategory`](#type-issuecategory) <code>&#124;</code> `undefined`||Category of the [Issue](#type-issue)|
|`description`|[`string`](#type-string) <code>&#124;</code> `undefined`||Description of the [Issue](#type-issue)|
|`doneRatio`|[`int32`](#type-int32)||Defaults to *zero*, only settable if no child issues exist|
|`dueDate`|[`date`](#type-date) <code>&#124;</code> `undefined`||Only settable if no child issues exist|
|`estimatedHours`|[`float32`](#type-float32) <code>&#124;</code> `undefined`||Estimated hours of the [Issue](#type-issue)|
|`isPrivate`|[`bool`](#type-bool)||Private State of the [Issue](#type-issue)|
|`issue`|[`Issue`](#type-issue)|required|[Issue](#type-issue) to update|
|`parent`|[`Issue`](#type-issue) <code>&#124;</code> `undefined`||Parent of the [Issue](#type-issue)|
|`priority`|[`IssuePriority`](#type-issuepriority)||Defaults to default priority, only settable if no child issues exist|
|`project`|[`Project`](#type-project)||[Project](#type-project) of the [Issue](#type-issue)|
|`startDate`|[`date`](#type-date)||Only settable if no child issues exist|
|`status`|[`IssueStatus`](#type-issuestatus)||Defaults to default status in tracker|
|`subject`|[`string`](#type-string)||Subject of the [Issue](#type-issue)|
|`tracker`|[`Tracker`](#type-tracker)||[Tracker](#type-tracker) of the [Issue](#type-issue))|

### <a name='type-updatemembership'></a> UpdateMembership


Updates an existing [Membership](#type-membership).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`addRoles`|`[`[`Role`](#type-role)`]`||Roles to be added to the [Membership](#type-membership), can not be set if 'roles' is set|
|`membership`|[`Membership`](#type-membership)|required|[Membership](#type-membership) to update|
|`removeRoles`|`[`[`Role`](#type-role)`]`||Roles to be removed of the [Membership](#type-membership), can not be set if 'roles' is set|
|`roles`|`[`[`Role`](#type-role)`]`||Roles of the [Membership](#type-membership), can not be set if 'addRoles' or 'removeRoles' is set|

### <a name='type-updateproject'></a> UpdateProject


Updates an existing [Project](#type-project).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)
* [`Membership`](#type-membership)
* [`Project`](#type-project)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`addCustomModules`|`[`[`string`](#type-string)`]`||Custom modules to be added to the [Project](#type-project), can not be set if 'customModules' is set|
|`addStandardModules`|`[`[`ProjectModule`](#type-projectmodule)`]`||Standard modules to be added to the [Project](#type-project), can not be set if 'standardModules' is set|
|`customModules`|`[`[`string`](#type-string)`]`||Custom modules of the [Project](#type-project), can not be set if 'addCustomModules' or 'removeCustomModules' is set|
|`description`|[`string`](#type-string) <code>&#124;</code> `undefined`||Description of the [Project](#type-project)|
|`inheritMembers`|[`bool`](#type-bool)||Inherit members state of the [Project](#type-project)|
|`isPublic`|[`bool`](#type-bool)||Is public state of the [Project](#type-project)|
|`name`|[`string`](#type-string)||Name of the [Project](#type-project)|
|`parent`|[`Project`](#type-project) <code>&#124;</code> `undefined`||Parent of the [Project](#type-project)|
|`project`|[`Project`](#type-project)|required|[Project](#type-project) to update|
|`removeCustomModules`|`[`[`string`](#type-string)`]`||Custom modules to be removed of the [Project](#type-project), can not be set if 'customModules' is set|
|`removeStandardModules`|`[`[`ProjectModule`](#type-projectmodule)`]`||Standard modules to be removed of the [Project](#type-project), can not be set if 'standardModules' is set|
|`standardModules`|`[`[`ProjectModule`](#type-projectmodule)`]`||[Modules](#type-projectmodule) of the [Project](#type-project), can not be set if 'addStandardModules' or 'removeCustomModules' is set|

### <a name='type-updateuser'></a> UpdateUser


Updates an existing [User](#type-user).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)
* [`Authentication`](#type-authentication)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`firstname`|[`string`](#type-string)||Firstname of the [User](#type-user)|
|`isAdmin`|[`bool`](#type-bool)||Is admin state of the [User](#type-user)|
|`lastname`|[`string`](#type-string)||Lastname of the [User](#type-user)|
|`login`|[`string`](#type-string)||Login of the [User](#type-user)|
|`mail`|[`string`](#type-string)||Mail of the [User](#type-user)|
|`status`|[`UserStatus`](#type-userstatus)||[UserStatus](#type-userstatus) of the [User](#type-user)|
|`user`|[`User`](#type-user)|required|[User](#type-user) to update|

### <a name='type-upload'></a> Upload


Appends an [Attachment](#type-attachment) to an [Issue](#type-issue).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`description`|[`string`](#type-string) <code>&#124;</code> `undefined`||Description of the [Upload](#type-upload)|
|`path`|[`string`](#type-string)|required|Filepath of the File to be uploaded|

### <a name='type-user'></a> User


Creates a Redmine [User](#type-user).

**Instantiable:** yes

**Permitted child items:**
* [`Choice`](#type-choice)
* [`DateInput`](#type-dateinput)
* [`LineInput`](#type-lineinput)
* [`MultiChoice`](#type-multichoice)
* [`TextInput`](#type-textinput)
* [`Authentication`](#type-authentication)

#### Properties

|Name|Type|Attributes|Description|
|:-|:-|:-|:-|
|`apiKey`|[`string`](#type-string) <code>&#124;</code> `restricted`|readonly|ApiKey of the [User](#type-user). Available when Identity user is an admin or the user.|
|`createdOn`|[`date`](#type-date)|readonly|Created date of the [User](#type-user)|
|`firstname`|[`string`](#type-string)|required|Firstname of the [User](#type-user)|
|`groups`|`[`[`Group`](#type-group)`]` <code>&#124;</code> `restricted`|readonly|Groups of the [User](#type-user). Available when Identity user is an admin.|
|`isAdmin`|[`bool`](#type-bool) <code>&#124;</code> `restricted`||Is admin state of the [User](#type-user). Available when Identity user is an admin or the user.|
|`lastLoginOn`|[`date`](#type-date) <code>&#124;</code> `undefined`|readonly|Last login on date of the [User](#type-user)|
|`lastname`|[`string`](#type-string)|required|Lastname of the [User](#user)|
|`login`|[`string`](#type-string)|required|Login of the [User](#type-user)|
|`mail`|[`string`](#type-string) <code>&#124;</code> `restricted`|required|Mail of the [User](#type-user). Available when Identity user is an admin or the user.|
|`memberships`|`[`[`Membership`](#type-membership)`]`|readonly|Memberships of the [User](#type-user)|
|`status`|[`UserStatus`](#type-userstatus) <code>&#124;</code> `restricted`||Current [UserStatus](#type-userstatus)|


## <a name='type-category-query'></a> Queries


### <a name='type-getcurrentdatetime'></a> GetCurrentDateTime

Returns the local system date.

**Requires Admin:** no

`GetCurrentDateTime(): date`

Return type: [`date`](#type-date)
### <a name='type-getcurrentuser'></a> GetCurrentUser

Retrieving the [User](#type-user) whose credentials are used to access the [REST API](https://www.redmine.org/projects/redmine/wiki/rest_api).

**Requires Admin:** no

`GetCurrentUser(): User`

Return type: [`User`](#type-user)
### <a name='type-getgroup'></a> GetGroup

Returns a single [Group](#type-group).

**Requires Admin:** yes

`GetGroup(id: int32): Group`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`id`|[`int32`](#type-int32)|Redmine id of group to return|||

`GetGroup(name: string): Group`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`name`|[`string`](#type-string)|Name of group to return|||

Return type: [`Group`](#type-group)
### <a name='type-getgroups'></a> GetGroups

Returns an array of [Groups](#type-group).

**Requires Admin:** yes

`GetGroups(): [Group]`

Return type: `[`[`Group`](#type-group)`]`
### <a name='type-getissue'></a> GetIssue

Returns a single [Issue](#type-issue).

**Requires Admin:** no

`GetIssue(id: int32): Issue`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`id`|[`int32`](#type-int32)|Redmine id of issue to return|||

Return type: [`Issue`](#type-issue)
### <a name='type-getissuecategory'></a> GetIssueCategory

Returns a single [IssueCategory](#type-issuecategory).

**Requires Admin:** no

`GetIssueCategory(id: int32): IssueCategory`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`id`|[`int32`](#type-int32)|Redmine id of issue category to return|||

Return type: [`IssueCategory`](#type-issuecategory)
### <a name='type-getissuepriorities'></a> GetIssuePriorities

Returns an array of [Issue Priorities](#type-issuepriority).

**Requires Admin:** no

`GetIssuePriorities(includeInactive: bool): [IssuePriority]`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`includeInactive`|[`bool`](#type-bool)|Defaults to `true`||4.1.0|

Return type: `[`[`IssuePriority`](#type-issuepriority)`]`
### <a name='type-getissuepriority'></a> GetIssuePriority

Returns a single [IssuePriority](#type-issuepriority).

**Requires Admin:** no

`GetIssuePriority(id: int32): IssuePriority`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`id`|[`int32`](#type-int32)|Redmine id of issue priority to return|||

`GetIssuePriority(name: string): IssuePriority`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`name`|[`string`](#type-string)|Name of group to return|||

Return type: [`IssuePriority`](#type-issuepriority)
### <a name='type-getissues'></a> GetIssues

Returns an array of [Issues](#type-issue) filtered by the specified parameters.

**Requires Admin:** no

`GetIssues(assignedTo: Group|User|undefined, project: Project|undefined, status: IssueStatus|IssueStatusFilter|undefined, tracker: Tracker|undefined): [Issue]`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`assignedTo`|[`Group`](#type-group) <code>&#124;</code> [`User`](#type-user) <code>&#124;</code> `undefined`|Assigned group or user of the issue, defaults to `undefined`|||
|`project`|[`Project`](#type-project) <code>&#124;</code> `undefined`|Project of the issue, defaults to `undefined`|||
|`status`|[`IssueStatus`](#type-issuestatus) <code>&#124;</code> [`IssueStatusFilter`](#type-issuestatusfilter) <code>&#124;</code> `undefined`|Issue status or status filter of the issue, defaults to `undefined`|||
|`tracker`|[`Tracker`](#type-tracker) <code>&#124;</code> `undefined`|Tracker of the issue, defaults to `undefined`|||

Return type: `[`[`Issue`](#type-issue)`]`
### <a name='type-getissuestatus'></a> GetIssueStatus

Returns a single [IssueStatus](#type-issuestatus).

**Requires Admin:** no

`GetIssueStatus(id: int32): IssueStatus`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`id`|[`int32`](#type-int32)|Redmine id of issue status to return|||

`GetIssueStatus(name: string): IssueStatus`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`name`|[`string`](#type-string)|Name of issue status to return|||

Return type: [`IssueStatus`](#type-issuestatus)
### <a name='type-getissuestatuses'></a> GetIssueStatuses

Returns an array of [Issue Statuses](#type-issuestatus).

**Requires Admin:** no

`GetIssueStatuses(): [IssueStatus]`

Return type: `[`[`IssueStatus`](#type-issuestatus)`]`
### <a name='type-getproject'></a> GetProject

Returns a single [Project](#type-project).

**Requires Admin:** no

`GetProject(identifier: string): Project`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`identifier`|[`string`](#type-string)|Redmine id of project to return|||

Return type: [`Project`](#type-project)
### <a name='type-getprojectgroup'></a> GetProjectGroup

Returns a single [Group](#type-group) in a [Project](#type-project).

**Requires Admin:** no

`GetProjectGroup(id: int32, project: Project): Group`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`id`|[`int32`](#type-int32)|Redmine id of group in project to return|||
|`project`|[`Project`](#type-project)|Project from which the group is retrieved|||

`GetProjectGroup(name: string, project: Project): Group`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`name`|[`string`](#type-string)|Group name of group in project to return|||
|`project`|[`Project`](#type-project)|Project from which the group is retrieved|||

Return type: [`Group`](#type-group)
### <a name='type-getprojectgroups'></a> GetProjectGroups

Returns an array of [Groups](#type-group) of a [Project](#type-project).

**Requires Admin:** no

`GetProjectGroups(project: Project): [Group]`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`project`|[`Project`](#type-project)|Project from which the groups are retrieved|||

Return type: `[`[`Group`](#type-group)`]`
### <a name='type-getprojectissuecategories'></a> GetProjectIssueCategories

Returns an array of [IssueCategories](#type-issuecategory) of a [Project](#type-project).

**Requires Admin:** no

`GetProjectIssueCategories(project: Project): [IssueCategory]`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`project`|[`Project`](#type-project)|Project from which the issue categories are retrieved|||

Return type: `[`[`IssueCategory`](#type-issuecategory)`]`
### <a name='type-getprojectissuecategory'></a> GetProjectIssueCategory

Returns a single [IssueCategory](#type-issuecategory) in a [Project](#type-project).

**Requires Admin:** no

`GetProjectIssueCategory(name: string, project: Project): IssueCategory`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`name`|[`string`](#type-string)|Name of issue category to return|||
|`project`|[`Project`](#type-project)|Project from which the issue category is retrieved|||

Return type: [`IssueCategory`](#type-issuecategory)
### <a name='type-getprojectmembership'></a> GetProjectMembership

Returns a single [Membership](#type-membership) in a [Project](#type-project).

**Requires Admin:** no

`GetProjectMembership(group: Group, project: Project): Membership`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`group`|[`Group`](#type-group)|[Group](#type-group) of which the membership is to be returned|||
|`project`|[`Project`](#type-project)|[Project](#type-project) from which the memberships are retrieved|||

`GetProjectMembership(project: Project, user: User): Membership`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`project`|[`Project`](#type-project)|[Project](#type-project) from which the memberships are retrieved|||
|`user`|[`User`](#type-user)|[User](#type-user) of which the membership is to be returned|||

Return type: [`Membership`](#type-membership)
### <a name='type-getprojects'></a> GetProjects

Returns an array of [Projects](#type-project).

**Requires Admin:** no

`GetProjects(): [Project]`

Return type: `[`[`Project`](#type-project)`]`
### <a name='type-getprojectuser'></a> GetProjectUser

Returns a single [User](#type-user) in a [Project](#type-project).

**Requires Admin:** no

`GetProjectUser(login: string, project: Project): User`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`project`|[`Project`](#type-project)|Project from which the user is retrieved|||
|`login`|[`string`](#type-string)|Redmine login of user to return|||

Return type: [`User`](#type-user)
### <a name='type-getprojectusers'></a> GetProjectUsers

Returns an array of [Users](#type-user) of a [Project](#type-project).

**Requires Admin:** no

`GetProjectUsers(project: Project): [User]`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`project`|[`Project`](#type-project)|Project from which the users are retrieved|||

Return type: `[`[`User`](#type-user)`]`
### <a name='type-getrole'></a> GetRole

Returns a single [Role](#type-role).

**Requires Admin:** no

`GetRole(id: int32): Role`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`id`|[`int32`](#type-int32)|Redmine id of role to return|||

`GetRole(name: string): Role`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`name`|[`string`](#type-string)|Name of role to return|||

Return type: [`Role`](#type-role)
### <a name='type-getroles'></a> GetRoles

Returns an array of [Roles](#type-role).

**Requires Admin:** no

`GetRoles(): [Role]`

Return type: `[`[`Role`](#type-role)`]`
### <a name='type-gettracker'></a> GetTracker

Returns a single [Tracker](#type-tracker).

**Requires Admin:** no

`GetTracker(id: int32): Tracker`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`id`|[`int32`](#type-int32)|Redmine id of tracker to return|||

`GetTracker(name: string): Tracker`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`name`|[`string`](#type-string)|Name of tracker to return|||

Return type: [`Tracker`](#type-tracker)
### <a name='type-gettrackers'></a> GetTrackers

Returns an array of [Tracker](#type-tracker).

**Requires Admin:** no

`GetTrackers(): [Tracker]`

Return type: `[`[`Tracker`](#type-tracker)`]`
### <a name='type-getuser'></a> GetUser

Returns a single [User](#type-user).

**Requires Admin:** no

`GetUser(id: int32): User`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`id`|[`int32`](#type-int32)|Redmine id of user to return|||

`GetUser(login: string): User`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`login`|[`string`](#type-string)|Redmine login of user to return|requiresadmin||

Return type: [`User`](#type-user)
### <a name='type-getusers'></a> GetUsers

Returns an array of [Users](#type-user) filtered by the specified parameters.

**Requires Admin:** yes

`GetUsers(group: Group|undefined, name: string|undefined, userStatus: undefined|UserStatus): [User]`

#### Parameters

|Parameter|Type|Description|Attributes|Minimum Redmine Version|
|:-|:-|:-|:-|:-|
|`group`|[`Group`](#type-group) <code>&#124;</code> `undefined`|Group of the user, defaults to `undefined`|||
|`name`|[`string`](#type-string) <code>&#124;</code> `undefined`|Name of the user, defaults to `undefined`|||
|`userStatus`|[`UserStatus`](#type-userstatus) <code>&#124;</code> `undefined`|User Status of the user, defaults to `undefined`|||

Return type: `[`[`User`](#type-user)`]`

## <a name='examples'></a> Examples

### Creating an Issue

```
Issue {
    id: issue
    assignedTo: GetCurrentUser()
    project: GetProject(identifier = "ProjectIdentifier")
    tracker: GetTracker(name = "Feature")
    subject: "Subject"
    description:
    |"This
    |"is
    |"a
    |"Description
}
```

### Updating an Issue

```
UpdateIssue {
    issue: GetIssue(id = 1)
    subject: "New Subject"

    Note {
        text: "Note text"
    }
}
```

### Creating an User

```
User {
    firstname: "Firstname"
    lastname: "Lastname"
    login: "Login"
    mail: "abc@example.com"

    Authentication {
        password: "12345678"
    }
}
```

