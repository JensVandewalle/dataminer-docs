---
uid: Cube_Main_Release_10.3.0
---

# DataMiner Cube Main Release 10.3.0 – Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!TIP]
> For release notes for this release that are not related to DataMiner Cube, see [General Main Release 10.3.0](xref:General_Main_Release_10.3.0).

## Highlights

#### Trending: New'Custom' button allows you to specify a custom X-axis range \[ID_31705\]

<!-- MR 10.3.0 - FR 10.2.1 -->

At the top of a trend graph, a new “Custom” button has been added next to the existing “Last 24 hours”, “Last week” and “Last month” buttons.

When you click this new button, you will be able to specify a custom X-axis range.

#### Visual Overview: Text wrapping and trimming \[ID_32440\]

<!-- MR 10.3.0 - FR 10.2.3 -->

In shapes linked to an object, it is now possible to change the text wrapping and trimming.

To do so, add a shape data field of type TextStyle, and set its value to “TextWrapping=...” and/or “TextTrimming=...” (separated by a pipe character).

| Shape data field | Value                                                                                       |
|------------------|---------------------------------------------------------------------------------------------|
| TextStyle        | TextWrapping=NoWrap/Wrap/WrapWithOverflow\|TextTrimming=CharacterEllipsis/WordEllipsis/None |

##### TextWrapping options

- **NoWrap**: The text will not wrap onto a new line, unless one was explicitly configured with a line break. Text that exceeds the bounds of the shape width and/or height will not be shown.

- **Wrap**: The text will automatically be wrapped onto new lines when the width of the shape is exceeded. The text past the boundaries of the shape height will not be shown.

- **WrapWithOverflow**: The text will be shown as before (default option).

##### TextTrimming options

- **CharacterEllipsis**: The text will be cut off a bit earlier than when TextTrimming is set to “None”, and “...” will be added to indicate that the text is longer than what fits in the shape.

- **WordEllipsis**: The text will be cut off at the nearest full word, and “...” will be added to indicate that the text is longer than what fits in the shape.

- **None**: The text will be cut off when necessary (default option).

> [!NOTE]
> Setting TextTrimming to either “CharacterEllipsis” or “WordEllipsis” will have no effect when TextWrapping is set to its default value (i.e. “WrapWithOverflow”).

#### Visual Overview - Edit in Visio: New options 'Add theming' and 'Add pretty hover' \[ID_32660\]

<!-- MR 10.3.0 - FR 10.2.5 -->

When, in DataMiner Cube, you right-click a visual overview and select “Edit in Visio”, an advanced edit panel will appear. When no shape is selected, you can now click an ellipsis button (“...”) in the top-right corner of the panel. This will open a menu with the following options.

- Add theming: If you click this option, the following theme options will be added to the page-level “Options” data field:

  *#000000=ThemeForeground\|#FF0000=ThemeAccentColor\|#FFFFFF=ThemeBackground*

- Add pretty hover: If you click this option, the following option will be added to the page-level “Options” data field:

  *HoverType=Geometry*

> [!NOTE]
> If no page-level “Options” data field exists, one will be created.

#### Services app: Service definition type \[ID_32667\]

<!-- MR 10.3.0 - FR 10.2.4 -->

When configuring a service definition, you now have to specify its type:

- SRM (default type)

- Skyline Process Automation

- Custom Process Automation

In Visual Overview, this type can be visualized by means of a \[ServiceDefinition:...\] placeholder. See the following example, in which xxx should be replaced by a service definition GUID.

```txt
[ServiceDefinition:xxx,Type]
```

> [!NOTE]
> It is not allowed to duplicate service definitions of type “Skyline Process Automation”. Therefore, the *Duplicate* option will not be available when you right-click a service definition of that type.

#### Visual Overview: Configuring a shape to set a duration in a session variable \[ID_32716\]

<!-- MR 10.3.0 - FR 10.2.4 -->

You can now configure a shape to set a duration of type TimeSpan in a session variable.

To do so, add the following shape data fields to the shape:

- a shape data field of type **SetVar**, of which the value is set to the name of the session variable, and

- a shape data field of type **SetVarOptions**, of which the value is set to “Control=Duration”, followed by the necessary options. For a list of possible options, see below.

| Shape data field | Value                                       |
|------------------|---------------------------------------------|
| SetVar           | \<name of session variable>                 |
| SetVarOptions    | Control=Duration\|\<option>\|\<option>\|... |

##### Options

Next to “Control=Duration”, you can specify the following options (separated by pipe characters).

| Option | Description |
|--|--|
| ShowInfinity=true/false | When this option is set to true, next to the duration selector, a checkbox is displayed that can be used to set the duration to infinity, which will replace the value of the session variable with TimeSpan.MaxValue. Default: False. |
| Minimum= | The minimum duration. Default: 1 minute. |
| Maximum= | The maximum duration. Default: 1 week. |

##### Setting the initial value of the duration in the session variable

Use a page-level InitVar field to set the initial value of the duration in the session variable.

If you set the initial value to “Infinity”, the value in the session variable will be replaced by TimeSpan.MaxValue. If the *ShowInfinity* option is set to true, a selected infinity checkbox will be displayed next to the duration selector.

> [!NOTE]
> Using an InitVar or SetVar field, it is possible to set a duration that is outside of the specified minimum/maximum range.

##### Specifying a duration

When specifying the minimum duration, the maximum duration and the InitVar value, you can use the following units:

| Unit    | Description                                                                               | Example |
|---------|-------------------------------------------------------------------------------------------|---------|
| No unit | If no unit is specified, then the number in question will be considered a number of days. | 1       |
| s       | seconds                                                                                   | 1s      |
| m       | minutes                                                                                   | 1m      |
| h       | hours                                                                                     | 1h      |
| d       | days                                                                                      | 1d      |
| mo      | months (1 month = 30 days)                                                                | 1mo     |
| y       | years (1 year = 365 days)                                                                 | 1y      |

#### Alarm Console - Automatic incident tracking: Manually add/remove alarms to/from alarm groups, move alarms from one alarm group to another, and rename alarm groups \[ID_32729\] \[ID_32819\] \[ID_32875\] \[ID_32914\] \[ID_32940\] \[ID_32957\] \[ID_33027\] \[ID_33036\] \[ID_33130\] \[ID_33212\]

<!-- MR 10.3.0 - FR 10.2.5
RN 33036/33130/33212: MR 10.3.0 - FR 10.2.6 -->

When, in the Alarm Console, you enable the “Automatic incident tracking” option, from now on, you will be able to manually add/remove alarms to/from alarm groups and to rename alarm groups.

- When you right-click an alarm that is not part of any alarm group, you will be able to click the “Add to incident” option. If you do so, a window will appear, asking you

  - to create a new incident (i.e. a new alarm group) and add the alarm to it, or

  - to add the alarm to an existing alarm group.

- When you right-click an alarm that is already part of an alarm group, you will be able to click the “Remove from incident” option. If you do so, the alarm will be removed from the alarm group of which it was a part.

- When you right-click an alarm that is part of an alarm group, you will be able to click the “Move to another incident” option. If you do so, a pop-up window will appear, asking you to either create a new incident or select another, existing incident.

- By default, automatically created alarm groups are named “View group:X” and manually created alarm groups are named “User defined group”. To rename an alarm group, click the pencil icon next to the name and enter a new name.

> [!NOTE]
>
> - From the moment a user manually adds or removes an alarm to or from an alarm group or renames an alarm group, that group will no longer be updated automatically.
> - Manually created incidents (alarm groups) will have their alarm focus score set to 0.
> - When Cube is connected to a DataMiner Agent that does not yet support manually creating, updating and renaming incidents (alarm groups), the menu commands to manipulate alarm groups will not be available.
> - See also [Alarm Console: Manually creating incident alarms even when “Automatic incident tracking” is disabled \[ID_33000\]](#alarm-console-manually-creating-incident-alarms-even-when-automatic-incident-tracking-is-disabled-id_33000)

#### Trending - Behavioral anomaly detection: New type of change point 'flatline' \[ID_32839\] \[ID_32856\] \[ID_32950\] \[ID_32993\] \[ID_33559\]

<!-- MR 10.3.0 - FR 10.2.5
RN 32993: MR 10.3.0 - FR 10.2.6
RN 33559: MR 10.3.0 - FR 10.2.8 -->

The DataMiner Analytics software can detect a number of changes in the behavior of a trend, also known as “change points”. From now on, it will also be able to detect change points of type “flatline”. A flatline is detected when a fluctuating value suddenly remains constant.

A change point of type flatline will be labeled anomalous when no flatline change point of approximately the same length or longer was recently detected in the trend of the parameter in question.

A running estimate will be kept of how long the parameter typically remains constant. If this estimate exceeds 1 hour, no change points of type “flatline” will be detected. Else, a change point of type “flatline” will be detected if the parameter value was not constant in the last hour but is constant again for more than 3 times the running estimate.

Whenever an anomalous flatline is detected, a “suggestion event” is generated. You can view these suggestion events by creating a suggestion event tab in the Alarm Console.

A new flatline trend icon will be used to indicate when a parameter has flatlined.

> [!NOTE]
> Flatline change points can also be detected for history set parameters that are set nearly in real time, i.e. parameters of which the incoming changes never have a delay larger than 10 minutes.

#### Visual Overview: ServiceManager component functionality expanded to support Process Automation UI \[ID_33187\]

<!-- MR 10.3.0 - FR 10.2.6
See also: Enhancements – Fix was moved to 10.2.0 CU3 by RN 33188 -->

To make it possible to show an overview of Process Automation service definitions in Visual Overview and filter these, the functionality of the *ServiceManager* component has been expanded.

##### interface=definitions component option

When you embed the Services module in Visio using the shape data field *Component* with the value *ServiceManager*, in the *ComponentOptions* shape data field, you can now use the option *interface=definitions* to only show the *Definitions* > *Recent* tab of the Services module. All existing options and variables have been made compatible with this option.

##### Filter shape data

If you use the *interface=definitions* component option described above, you can now also combine a *Filter* shape data field with the *ServiceManager* component. This allows you to filter the service definitions in the list, in the same way as in a *ListView* component. The following properties are supported for the filter:

- Name (String)

- Description (String)

- IsTemplate (Boolean)

- ID (GUID)

- CreatedBy (String)

- CreatedAt (DateTime)

- LastModifiedBy (String)

- LastModified (DateTime)

- NodeFunctionIDs (List\<Guid>)

- Properties (IDictionary\<string, dynamic>)

- ServiceDefinitionType (Int): This is an enum with the following possible values:

  - 0 = Default (representing the type "SRM" in Cube)

  - 1 = ProcessAutomation (representing the type "Skyline Process Automation" in Cube)

  - 2 = CustomProcessAutomation (representing the type "Custom Process Automation" in Cube)

Examples:

- This filter will only show service definitions of type "Skyline Process Automation" or "Custom Process Automation":

    | Shape data field | Value                                                                                                            |
    |--------------------|------------------------------------------------------------------------------------------------------------------|
    | Filter             | ServiceDefinition.ServiceDefinitionType\[Int32\] == 1 \|\| ServiceDefinition.ServiceDefinitionType\[Int32\] == 2 |

- This filter will only show service definitions with the property *Virtual Platform* set to VPA:

    | Shape data field | Value                                                    |
    |--------------------|----------------------------------------------------------|
    | Filter             | ServiceDefinition.Properties."Virtual Platform" == "VPA" |

##### New HideAddButton and HideDeleteButton component options

The following options can now also be specified in the *ComponentOptions* shape data field for a *ServiceManager* component:

- **HideAddButton=**: If this option is set to "true", no options to add a service definition will be displayed.

- **HideDeleteButton=**: If this option is set to "true", no options to delete a service definition will be displayed.

#### Desktop app - Start window: New 'HTTP or HTTPS' setting \[ID_33289\]

<!-- MR 10.3.0 - FR 10.2.6 -->

Up to now, when a DataMiner Agent had been added to the start window of the DataMiner Cube desktop app at a time when only HTTP was available, Cube would no longer switch to HTTPS when that protocol became available and HTTP got blocked.

When you add a DataMiner Agent to the start window, in the Advanced settings, you can now set the *Transport* setting to either “HTTPS only” or “HTTP or HTTPS”. If you choose the latter option, Cube will use HTTP by default. When HTTP is not available, it will try to use HTTPS instead. From that point onwards, the transport setting will automatically be switched to “HTTPS only”, so HTTPS will be used for all following sessions.

> [!NOTE]
> If a DataMiner Agent is configured to use only HTTPS, Cube will not fall back to HTTP, even when you have chosen the “HTTP or HTTPS” option.

#### Visual Overview: Adding a 'Refresh' and/or a 'Sort' button to a table control \[ID_33346\]

<!-- MR 10.3.0 - FR 10.2.6 -->

When using a shape of type *ParameterControls* to visualize a table in a Visio drawing, you can now add a *Refresh* button and/or a *Sort* button to that shape.

Example of how to add both a *Refresh* button and a *Sort* button:

1. Create three shapes and group them:

   - the first shape will contain the table,

   - the second shape will contain the *Refresh* button, and

   - the third shape will contain the *Sort* button.

1. Add the following shape data field to the shape that has to contain the table:

   | Shape data field      | Value |
   |-------------------------|-------|
   | ParameterControlOptions | Table |

1. Add the following shape data field to the shape that has to contain the Refresh button:

   | Shape data field      | Value   |
   |-------------------------|---------|
   | ParameterControlOptions | Refresh |

1. Add the following shape data field to the shape that has to contain the Sort button:

   | Shape data field      | Value |
   |-------------------------|-------|
   | ParameterControlOptions | Sort  |

1. Add the following shape data fields to the group:

   | Shape data field | Value                      |
   |--------------------|----------------------------|
   | Element            | Element ID or element name |
   | ParameterControl   | ID of the table parameter  |

> [!NOTE]
> The *Refresh* button and the *Sort* button will only be displayed when necessary.

#### Alarm Console: Updating incidents using the side panel \[ID_33436\]\[ID_33450\]

<!-- MR 10.3.0 - FR 10.2.7 -->

In the Alarm Console, it is now possible to edit incidents (i.e. alarm groups) using the side panel.

When you open the side panel and select an incident, a *Drag-and-drop editing* button will appear. Clicking that button will freeze both the side panel and the alarm tab and will allow you to

- add alarms to the incident by dragging them from the Alarm Console onto the side panel, and

- remove alarms from the incident by clicking the “X” next to the base alarm.

When you are finished editing the incident, click *Apply* to apply your changes and unfreeze the side panel.

> [!NOTE]
> Instead of opening the side panel and clicking the *Drag-and-drop editing* button, you can also right-click an incident and select *Edit incident*. This will open the side panel (if it is not open yet) and enable the “drag and drop” mode.

#### Tab layout: Closing a card tab by clicking it with the middle mouse button \[ID_33883\]

<!-- MR 10.3.0 - FR 10.2.9 -->

When the card layout is set to “tab layout”, you can now close a card tab by clicking it with the middle mouse button.

#### Password box with strength indicator and peek button \[ID_33937\]

<!-- MR 10.3.0 - FR 10.2.9 -->

Password boxes in Cube will now indicate the password strength (common, very weak, weak, good, strong, very strong) based on a scoring algorithm and a dictionary of default and well-known passwords. They will also have a peek button that allows you to temporarily reveal the password you have entered.

These new password boxes can be found in the following locations:

- Cube login screen (peek only)
- Data Display: parameters of type password (e.g. the password box of a Microsoft Platform element)
- Edit port settings of an SNMPv3 element
- System Center \> Agents \> Add
- System Center \> Database
- System Center \> Users/groups \> Add new user... (peek only)
- System Center \> System Settings \> Credentials Library
- System Center \> System Settings \> LDAP
- Interactive Automation scripts (UIBlock of type PasswordBox)

> [!NOTE]
>
> - If a value received from the server has been automatically entered in a password box, the strength indicator and peek button will not be available until you enter a completely new password.
> - If the value received from the server is a fixed 8-asterisk-long placeholder instead of an actual password, you will not be able to modify it. You will be forced to replace the entire value.

#### New 'Light' theme & new links in the Apps list \[ID_33944\]

<!-- MR 10.3.0 - FR 10.2.9 -->

A new theme has been added to DataMiner Cube: “Light”.

Also, the Apps list now contains links to the Catalog, the Cloud Admin app and custom web apps.

## Other new features

#### Visual Overview: Shape data fields of type 'ParametersSummary' can now also handle subscription filters specified in the index part of a parameter section \[ID_31609\]

<!-- MR 10.3.0 - FR 10.2.1 -->

The value of a ParametersSummary shape data field has to consist of a number of delimited sections:

```txt
Operation|Param1|Param2|...|ParamZ|Actions
```

Each parameter section in the value above has to be configured as follows:

```txt
Element:Parameter:Index
```

From now on, the “Index” part of a parameter section can also contain a subscription filter:

```txt
Filter=<subscriptionFilter>
```

This subscription filter can be any filter that can be passed to a parameter change subscription (e.g. “VALUE=\<pid> == \<value>”, “fullFilter=(...)”, etc.).

> [!NOTE]
> Up to now, when the index part of a parameter section contained a wildcard, no results would be returned whenever cells were set to “not initialized”. From now on, cells set to “not initialized” will be skipped.

#### Trending: New 'Fixed interval' option when exporting average trend data \[ID_31699\]

<!-- MR 10.3.0 - FR 10.2.2 -->

When you export average trend data, selecting the new *Fixed interval* option will make sure that the data points are equally distributed and that gaps smaller than a time slot (e.g. 5 minutes) are ignored.

> [!NOTE]
>
> - The “fixed interval” option can only be used when exporting average trend data for double, number or analog parameters.
> - When you select the *Fixed interval* option, the *Exclude gaps* option will automatically be selected and disabled to indicate that the latter option is included in the former.
> - When you select the *Line graph* option, from now on, that option will no longer add intermediary data points. Those will now by default be added when you select the *Fixed interval* option.

#### DataMiner Cube: Start window will now detect a HTTP(S) redirection and will ask the user to confirm that redirection \[ID_31726\]

<!-- MR 10.3.0 - FR 10.2.1 -->

When, in the start window of the DataMiner Cube desktop app, you try to connect to a DataMiner Agent with a redirection on HTTP(S) level, you will now be asked to confirm the redirection.

#### Visual Overview - Embedded Resource Manager component: New and updated session variables \[ID_31770\] \[ID_32394\]

<!-- RN 31770: MR 10.3.0 - FR 10.2.1
RN 32394: MR 10.3.0 - FR 10.2.3 -->

The following changes have been made with regard to session variables that can be used in embedded Resource Manager components.

##### New variable 'SelectedTimeRange'

When you select a time range, that range will be stored in the SelectedTimeRange variable.

The value can be set in serialized form (e.g. “5248098399646517511;5248392353962787511”) or using a “start;stop” format. In the latter case, start and stop must be timestamps that can be parsed by DateTime (e.g. “2017-09-17T09:42:01.9129607Z;2018-08-23T15:05:53.5399607Z” in ISO 8601 format, or “17/09/2017 9:42:01;23/08/2018 15:05:53” in local format).

This variable will be cleared whenever you select another time range in the timeline.

##### Updated variable 'SelectedResource'

The SelectedResource variable will now also be filled in when you select a resource band.

Note that, when you select a resource band, the SelectedPool variable will contain the first pool of the selected resource.

##### Problem with 'SelectedReservation' variables

When you select a booking, the following variables are filled in:

- SelectedReservation
- SelectedReservationDefinition
- ResourcesInSelectedReservation
- TimerangeOfSelectedReservation

However, up to now, when the current booking selection was cleared, those variables would incorrectly not get cleared.

#### Visual Overview: Specifying a remote debugging port for Chromium and Edge browser engines \[ID_31792\]

<!-- MR 10.3.0 - FR 10.2.4 -->

Embedded Chromium and Edge browser engines allow external tooling to inspect and manipulate their web browser.

When starting DataMiner Cube, from now on, you can pass a remote debugging port for both Chromium and Edge engines by specifying the following command line options:

- ChromeRemoteDebuggingPort=7001
- EdgeRemoteDebuggingPort=7002

Note that the port number must be between 1024 and 65535.

#### Alarm templates - Information events: Support for wildcard values \[ID_31872\] \[ID_32106\]

<!-- MR 10.3.0 - FR 10.2.2 -->

In the alarm template editor, you can indicate that an information event should be generated when a certain parameter reaches a certain value. To do so, you select the *Info* option and enter a value in the text box or, in case of a discreet parameter, select a value in the selection box.

From now on, for parameters of type string or double, it is also possible to enter values that contain a wildcard (\* or ?).

#### Visual Overview: Resource placeholder can now be used to check whether a resource is in use \[ID_32203\]

<!-- MR 10.3.0 - FR 10.2.3 -->

The \[Resource:...\] placeholder can be used to retrieve a property of a resource. From now on, it can also be used to check whether a resource is being used by any bookings. To do so, use the following syntax.

```txt
[Resource:<GUID>,InUse]
```

> [!NOTE]
> Currently, this check will only be performed when the visual overview is opened or when the GUID or the resource itself is changed.

See also: [New 'IN USE' info tag to be used in element shapes linked to resources \[ID_32393\]](#new-in-use-info-tag-to-be-used-in-element-shapes-linked-to-resources-id_32393)

#### Visual Overview: Linking a shape to an alarm filter with a System Name or System Type filter context \[ID_32252\] \[ID_32548\]

<!-- RN 32252: MR 10.3.0 - FR 10.2.3
RN 32548: MR 10.3.0 - FR 10.2.4 -->

When you link a shape to an alarm filter, you can specify a filter context. Up to now, it was possible to filter on element, service or view. Now, it is also possible to filter on EPM system name or system type using the following syntax:

```txt
FilterContext=SystemName=X
FilterContext=SystemType=X
```

If you specify a filter context like the one above, the shape will be linked to the alarms of which the “System Name” or “System Type” property is set to “X”. This will allow you, for example, to show the alarm statistics of an EPM object or to create a new alarm tab by clicking the shape in question.

> [!NOTE]
> It is also possible to specify a filter context in which both system name and system type are combined. To do so, use the following syntax:
>
> *FilterContext=SystemName=X;SystemType=Y*
>
> If you specify a filter context like the one above, the shape will be linked to the alarms of which the “System Name” is set to “X” and “System Type” is set to “Y”.

#### Visual Overview: Use of dynamic units now depends on value of DynamicUnits soft-launch option \[ID_32256\]

<!-- MR 10.3.0 - FR 10.2.3 -->

Up to now, when configuring a parameter shape, it was possible to enable to use of dynamic units (i.e. units that can be converted to other units according to rules configured in the protocol) by adding “DynamicUnits=true” in an Options data field. From now on, when you do not specify this option in a parameter shape, whether or not that shape will use dynamic unit will depend on the value of the DynamicUnits soft-launch option.

> [!NOTE]
> The DynamicUnits=true/false option can now be used to override the value of the DynamicUnits soft-launch option. For example, if the DynamicUnits soft-launch option is set to true, you can configure a parameter shape to not use dynamic units by adding "DynamicUnits=False" to its Options data field.
>
> For more information on soft-launch options, see [Soft-launch options](xref:SoftLaunchOptions).

#### Data Display: Support for launching EPM objects by clicking buttons in Data Display table cells \[ID_32368\] \[ID_33295\] \[ID_33857\]

<!-- RN 32368: MR 10.3.0 - FR 10.2.3
RN 33295: MR 10.3.0 - FR 10.2.6
RN 33857: MR 10.3.0 - FR 10.2.9 -->

This feature offers a new way of adding links to EPM objects in a Data Display table.

When, in a protocol, you configure a cell button as shown below, the table cell will display the SystemType and SystemName defined in the EPM object. Clicking the link will open a new card for that object.

Example:

```xml
<Measurement>
  <Type>button</Type>
  <Discreets>
    <Discreet>
      <Display>{linkedItemName}</Display>
      <Value type="open">{pid:530}</Value>
    </Discreet>
  </Discreets>
</Measurement>
```

The discreet value can contain the SystemType and SystemName of the object, or a reference like “{pid:530}”. In the example above, the identifier is stored in the column with parameter ID 530, which can be the read parameter of the same column or a different column.

If you know the type of the EPM object, you can add a type prefix (epm or view), followed by an equal sign and (a reference to) the identifier.

The \<Display> tag of the discreet can contain the same references as the \<Value> tag. One extra keyword is possible (and recommended): {linkedItemName}. This keyword will be replaced with the name of the object referred to in the \<Value> tag.

If you want to specify the page to be selected by default, add a suffix to the identifier in the \<Value> tag containing the root page name and the page name, separated by a colon. See the following examples:

- EPM=Cable/SF Cable1:Topology:Total
- VIEW=436:BelowThisObject:STB
- VIEW=436:BelowThisView:Elements

If the SystemName contains colons (e.g. a MAC address), then replace the default separator (i.e. colon) by another one (e.g. a pipe character) by placing a \[sep:XY\] prefix in front of the SystemName. See the following example:

```xml
<Value type="open">{EPM=[sep::|]CPE/00:01:08:01:08:01|DATA|CPE Frequencies}</Value>
```

Moreover, you can specify a second custom separator to also replace the existing separator inside the SystemType and/or SystemName. Since the default separator between the SystemType and the SystemName is “/”, this would mean that neither the systemType nor the SystemName would be allowed to contain that character (“/”).

In the following example, a second \[sep:XY\] is used to replace the “/” inside the SystemType (“CPE/CPE”) with another character (“$”).

```xml
<Value type="open">{EPM=[sep::|][sep:/$]CPE/CPE$00:01:08:01:08:01|DATA|CPE Frequencies}</Value>
```

In short,

- the first \[sep:XY\] will replace the separator between the arguments, and
- the second \[sep:XY\] will replace the separator inside the SystemType and/or SystemName.

If you want to replace the separator inside the name, you must specify both the first \[sep:XY\] and the second \[sep:XY\], even if there are no arguments.

> [!NOTE]
>
> - In each of the examples above, the card will be opened on a particular page:
>   - “Topology:Total” or “t:Total” will open the topology page named “Total”.
>   - “BelowThisObject:STB” or “bto:STB” will open the CPE card page named “STB”.
>   - “BelowThisView:Elements” or “btv:Elements” will open the view card page named “Elements”.
> - When the card layout is set to “Tab layout”, it is now possible to save EPM cards in workspaces.

#### New 'IN USE' info tag to be used in element shapes linked to resources \[ID_32393\]

<!-- MR 10.3.0 - FR 10.2.3 -->

Shapes that are linked to an element can automatically be linked to corresponding resources by adding “UseResource=True” in a shape data field of type Options.

From now on, in shapes linked to resources, you can specify “IN USE” in a shape data field of type Info. That way, the shape will indicate whether the linked resource is in use. However, note that for this feature to work, the shape text has to contain a “\*” character.

Alternatively, you can also use “\[In use\]” in any dynamic part specified in either a shape data field or the shape text.

See also: [Visual Overview: Resource placeholder can now be used to check whether a resource is in use \[ID_32203\]](#visual-overview-resource-placeholder-can-now-be-used-to-check-whether-a-resource-is-in-use-id_32203)

#### Visual Overview: Shapes that cannot be clicked and had their text trimmed will show a tooltip with the full shape text \[ID_32463\]

<!-- MR 10.3.0 - FR 10.2.4 -->

Shapes that cannot be clicked and had their text trimmed by means of a “TextTrimming” option in a shape data field of type TextStyle will now automatically show a tooltip with the full, untrimmed shape text.

#### New setting to enable the cache of the Chromium browser engine \[ID_32534\]

<!-- MR 10.3.0 - FR 10.2.4 -->

In the *Computer \> Advanced* section of the *Settings* app, you can now use the *Enable browser cache* setting to enable the cache of the Chromium browser engine.

Enabling this cache has the following advantages:

- Certain web applications will load faster.
- SAML authentication can provide a better single sign-on experience.

> [!CAUTION]
> This feature involves a potential security risk. If multiple DataMiner users share the same Windows account on a particular computer, they will also share the same browser cache and, as a consequence, the same authentication on third-party websites.

#### Trending: Refresh rate of trend graphs can now be configured \[ID_32715\]

<!-- MR 10.3.0 - FR 10.2.4 -->

Up to now, open trend graphs were automatically refreshed every 2 minutes. From now on, you can specify a custom refresh rate (5 seconds to 5 minutes) in the *Update interval* setting, located in the *User \> Trending* section of the *Settings* app.

Default: 2 minutes

> [!NOTE]
>
> - Changing this refresh rate can have a minor effect on overall performance, especially when opening trend graphs with more than 10 parameters.
> - If you change the *Update interval* setting, then open trend graphs need to be closed and re-opened if you want them to use the new interval.

#### Visual Overview: Passing Interactive Automation script output to session variables \[ID_32874\]

<!-- MR 10.3.0 - FR 10.2.6 -->

Similar to regular Automation scripts, interactive Automation scripts are now also able to pass their output to session variables in Visual Overview.

> [!NOTE]
> When configuring the Execute shape, it is recommended to specify both the NoConfirmation option and the CloseWhenFinished option in the value of the Execute data field.

#### Visual Overview - Resource Manager component: Enhancements with regard to selecting bookings in the timeline \[ID_32938\]

<!-- MR 10.3.0 - FR 10.2.6 -->

A number of enhancements have been made with regard to selecting bookings in the timeline area of an embedded Resource Manager component.

- When you select a booking, the corresponding resource band and all occurrences of that booking will be selected.
- When you unselect a booking, the corresponding resource band and all occurrences of that booking will also be unselected.
- The reservation variable and the resource variable will always contain the booking and the resource selected in the timeline.
- When you remove a resource band, the corresponding resource variable will be cleared.

#### DataMiner Cube - Alarm Console: Users can now manually create incidents even when 'Automatic incident tracking' is disabled in System Center \[ID_32990\] \[ID_33354\]

<!-- MR 10.3.0 - FR 10.2.7 -->

From now on, users will be able to manually create incidents even when “Automatic incident tracking” is disabled in System Center.

#### Alarm Console: Manually creating incident alarms even when 'Automatic incident tracking' is disabled \[ID_33000\]

<!-- MR 10.3.0 - FR 10.2.6 -->

From now on, in the Alarm Console, you will be able to manually create incident alarms (i.e. alarm groups) even when the “Automatic incident tracking” option is disabled.

- When you right-click an alarm that is not part of any alarm group, you will be able to click the “Add to incident” option. If you do so, a window\* will appear, asking you

  - to create a new incident (i.e. a new alarm group) and add the alarm to it, or

  - to add the alarm to an existing alarm group.

These manually created groups will always be visible in active alarm tabs, even when the “Automatic incident tracking” option is disabled.

*\*This window lists all existing incidents. From now on, you will be able to sort this list by clicking a column header. Also, a search box has now been added to allow you to search for a particular incident.*

See also [Alarm Console - Automatic incident tracking: Manually add/remove alarms to/from alarm groups, move alarms from one alarm group to another, and rename alarm groups \[ID_32729\] \[ID_32819\] \[ID_32875\] \[ID_32914\] \[ID_32940\] \[ID_32957\] \[ID_33027\] \[ID_33036\] \[ID_33130\] \[ID_33212\]](#alarm-console---automatic-incident-tracking-manually-addremove-alarms-tofrom-alarm-groups-move-alarms-from-one-alarm-group-to-another-and-rename-alarm-groups-id_32729-id_32819-id_32875-id_32914-id_32940-id_32957-id_33027-id_33036-id_33130-id_33212)

#### Visual Overview: Resource usage now updated in real time \[ID_33001\] \[ID_33156\] \[ID_33497\]

<!-- MR 10.3.0 - FR 10.2.6 -->

From now on, resource usage will be updated in real time. This means that “\[Resource:\<GUID>,InUse\]” placeholders and Info data fields of type “IN USE” will now be updated without having to close and re-open cards.

Also, from now on, “\[Resource:\<GUID>,InUse\]” placeholders and Info data fields of type “IN USE” can be used in any element shape, provided it has “UseResource=True” in a shape data field of type Options.

#### Alarm Console: Additional actions to be performed on incidents \[ID_33056\]

<!-- MR 10.3.0 - FR 10.2.6 -->

From now on, when you right-click an incident (alarm group), you will be able to perform the following additional actions:

- Take ownership
- Release ownership
- Force release ownership
- Add a comment

If you right-click a manually created incident, you will also be able to select *Clear alarm*. When you clear a manually created incident, the alarm group will be cleared and all the base alarms will again be added to the Alarm Console.

#### Alarm templates - Anomaly detection: Configuring alarms for flatline changes \[ID_33123\] \[ID_33139\] \[ID_33171\]

<!-- MR 10.3.0 - FR 10.2.6 -->

From DataMiner 10.0.3 onwards, you can configure an alarm template so that alarms are generated instead of suggestion events when anomalies are detected for specific parameters. From now on, you can also enable this for flatline changes.

1. Click the cogwheel button in the top-right corner of the alarm template editor.
1. Select the option *Advanced configuration of anomaly detection*. Four extra columns will be displayed in the template editor.
1. In the *Flatline monitor* column, click the toggle button to enable or disable alarms for flatline changes.

#### Alarm Console: Second-generation hyperlinks of type 'openview', 'openservice', 'openelement' and 'openparameter' now support '\[PROPERTY:\]' keywords \[ID_33166\]

<!-- MR 10.3.0 - FR 10.2.7 -->

Up to now, it was only possible to use “\[PROPERTY:\]” keywords in second-generation hyperlinks of type “url”, “execute” and “script”. From now on, these keywords can also be used in second-generation hyperlinks of type “openview”, “openservice”, “openelement” and “openparameter”.

For example, a hyperlink of type “openelement” could contain the following content:

```txt
[PROPERTY:ALARM:Booking Manager Element ID]
```

> [!NOTE]
>
> - If you want to use a view property, a service property or an element property in a hyperlink, then you must enable its “Make this property available for alarm filtering” setting in DataMiner Cube.
> - If you want to use a view property on an alarm of an element that has been added to multiple views, the property that will be used in the hyperlink will be the property of the view with the lowest ID that contains the element.

#### Alarm Console: Assigning a ticket to an incident (alarm group) \[ID_33199\]

<!-- MR 10.3.0 - FR 10.2.6 -->

In the Alarm Console, it is now possible to assign tickets to incidents (alarm groups).

- To assign a ticket to an incident, right-click the incident (alarm group) and select *Ticket \> New*.

- To view a ticket assigned to an incident, right-click the incident (alarm group), select *Ticket*, and then select the ticket you want to view.

#### DataMiner Cube: Start window enhancements \[ID_33219\]

<!-- MR 10.3.0 - FR 10.2.6 -->

A number of enhancements have been made to the start window of the DataMiner Cube desktop app:

- Settings menu (cogwheel icon in bottom-right corner)

  - New *About* box with version information.

  - All menu items now have icons in front of them.

- When you right-click an agent,

  - you can now click *Open in browser* to connect to that agent using a browser version of Cube, and

  - all context menu items now have icons in front of them.

- When agents/clusters are arranged in named groups, the context menu of the DataMiner Cube system tray icon will now contain submenus per named group.

- The message that is displayed after a start window update will no longer show any technical information.

#### Anomaly alarms will now be triggered for all behavioral changes of monitored anomaly type \[ID_33281\]

<!-- MR 10.3.0 - FR 10.2.6 -->

When you enable alarm monitoring for a specific type of anomaly in an alarm template, it is now assumed that you wish to be alerted to all behavioral changes of that type. Previously, an alarm was only triggered in case the behavioral change was sufficiently significant with respect to other behavioral changes in the recent history of the parameter. Now behavioral changes of a specific type on a trended parameter will always be considered to be behavioral anomalies if anomaly monitoring is enabled on this type and parameter, even if the behavioral change point is not significantly different from other behavioral changes in the recent history of the trended parameter.

#### Data Display: Context menu of URL parameters now contains copy commands \[ID_33321\]

<!-- MR 10.3.0 - FR 10.2.6 -->

In Data Display, the context menu of a URL parameter will now contain the following copy commands:

- Copy ‘\<URL>’: Copies the URL to the Windows Clipboard.

- Copy value to editor: Copies the URL to the write parameter edit box.

  > [!NOTE]
  > This command will only be available when there is a write parameter.

#### Alarm Console: A comment will now be added to an manually created incident when created or updated \[ID_33387\]

<!-- MR 10.3.0 - FR 10.2.7 -->

When users manually create an incident, change the display value of a manually created incident or add or remove base alarms to or from a manually created incident, from now on, a comment will be added to the incident (Created, Base alarm added, Base alarm removed, Value changed by \<user name> @ \<time>).

#### Visual Overview - Resource Manager component: Passing elements, services or views using the YAxisResources variable \[ID_33402\]

<!-- MR 10.3.0 - FR 10.2.8 -->

From now on, you can pass elements, services, or views to the YAxisResources session variable in order to show the corresponding resource bands.

##### Passing elements

You can pass elements by name or by ID as a string of comma-separated values.

In case an element is configured as an element reference in a resource, as a main DVE element in a function resource, or as the element corresponding with a virtual function resource, the corresponding resource will be shown.

In the following example, three elements are passed: an element with the name "MyElement", the element to which the Visio drawing is linked, and the element with ID 123/456:

```txt
YAxisResources:Element=MyElement,[this element],123/456
```

The corresponding resource bands are not updated automatically in case there is a change to the configuration of the elements.

##### Passing services

You can pass services by name or by ID as a string of comma-separated values.

The resources of the bookings linked to the services will be shown.

In the following example, three services are passed: a service with the name “MyService”, the service to which the Visio drawing is linked, and the service with ID 123/456:

```txt
YAxisResources:Service=MyService,[this service],123/456
```

To also show resources for contributing bookings, in the ComponentOptions shape data field of the Resource Manager component, specify Recursive=True.

The resource band will be updated in real time, based on the linked booking. This means that when you add or remove resources in a booking, you will immediately see the effect on the timeline.

##### Passing views

You can pass views by name or by ID as a string of comma-separated values.

When you pass a view, for any elements in that view that are configured as an element reference in a resource, as a main DVE element in a function resource, or as the element corresponding with a virtual function resource, the corresponding resources will be shown.

In the following example, three views are passed: a view with the name "MyView", the view to which the Visio drawing is linked, and the view with ID 123:

```txt
YAxisResources:View=MyView,[this view],123
```

To also show resources for elements in child views, in the ComponentOptions shape data field of the Resource Manager component, specify Recursive=True.

The corresponding resource bands are not updated automatically in case there is a change to the configuration of the elements.

#### Failover: Current Failover DMA status will now automatically be refreshed every minute \[ID_33426\]

<!-- MR 10.3.0 - FR 10.2.8 -->

In the *Failover Config* window as well as the *Status* dialog box, the current Failover DMA status will now automatically be refreshed every minute.

#### Visual Overview - Service Manager component: Filtering on FunctionDefinitionType \[ID_33466\]

<!-- MR 10.3.0 - FR 10.2.7 -->

When you embed a Service Manager component in Visual Overview, it is now possible to apply a filter that will make the function tree only list functions with specific FunctionDefinitionType fields.

To do so, add a FunctionTypes option to the ComponentOptions shape data field.

| Shape data field | Value |
|--|--|
| Component | ServiceManager |
| ComponentOptions | FunctionTypes=\[comma-separated list of values\]<br> Possible values:<br> - Undefined (i.e. NULL value)<br> - UserTask<br> -  ScriptTask<br> - ResourceTask<br> - Gateway<br> - NoneStartEvent<br> - TimeStartEvent<br> - EndEvent |

> [!NOTE]
>
> - The FunctionTypes option
>   - only works in conjunction with the options Interface=definition or Interface=definitions.
>   - can be used in combination with the HideChildFunctions option.
>   - can be set dynamically using session variables.
> - The filter will be cleared when no FunctionTypes option is specified or when the FunctionTypes option is set to an empty list of values.
> - Parent functions that do not match the filter but have child functions that match the filter will be displayed in the function tree to allow you to navigate to one of the child functions.

#### Visual Overview - Resource Manager component: Selecting multiple resource bands in the timeline \[ID_33536\]

<!-- MR 10.3.0 - FR 10.2.8 -->

In the timeline of an embedded Resource Manager component, it is now possible to select multiple resource bands.

To select more than one resource band, click one, and then click another while holding down the CTRL key, etc. To select a list of consecutive resource bands, click the first one and then click the last one while holding down the SHIFT key.

When you select more than one resource band, the SelectedResource session variable will contain the GUIDs of all selected resources, separated by commas.

#### Visual Overview - Resource Manager component: Enhanced way of selecting a time range \[ID_33580\]

<!-- MR 10.3.0 - FR 10.2.8 -->

In the timeline, the context menu will no longer open automatically after selecting a time range by means of drag-and-drop. Instead, it will now only open when you right-click.

This change in behavior will now allow you to trigger a script by clicking an action button instead of selecting an option in the context menu of the timeline. In other words, you will now be able to proceed as follows:

1. Select a resource band.
1. Select a time range.
1. Click an action button.

The SelectedTimeRange variable will now be cleared when the time selection is cleared (i.e. when it is no longer visible/available). Up to now, this variable would only be cleared when the selection was changed.

#### System Center - Agents: BPA Details window now has a Copy button that copies the list of errors to the Windows clipboard \[ID_33638\]

<!-- MR 10.3.0 - FR 10.2.8 -->

When, in the *BPA* tab of the *Agents* section, you see a BPA test that returned errors during its last run, you can click “...” to open a *Details* window listing those errors.

At the bottom of this *Details* window, you can now find a *Copy* button that allows you to copy the list of errors to the Windows clipboard.

#### Visual Overview: \[this reservationID\] placeholder \[ID_33669\]

<!-- MR 10.3.0 - FR 10.2.8 -->

In shape data or shape text of shapes linked to a booking (e.g. dynamically generated shapes that represent bookings), you can now use a \[this reservationID\] placeholder to retrieve the GUID of the booking.

See the following examples:

`[Resource:[reservation:[this reservationID],ResourceID|NodeID=18|],Name]`

`[reservation:[this reservationID],Property=Monitoring]`

#### Alarm Console - Incident tracking: Some types of alarms can now be manually added to incidents even when they do not contain any focus data \[ID_33771\] \[ID_33803\]

<!-- MR 10.3.0 - FR 10.2.9 -->

Up to now, alarms that did not contain any focus information were not allowed to be the base alarm of an incident. From now on, alarms that do not contain any focus data can be manually added to an incident, provided they are not one of the following types of alarms:

- correlation alarms
- clearable alarms
- information events
- suggestion events
- other incidents

#### Trending: Prediction type selection has now moved to the context menu \[ID_33861\]

<!-- MR 10.3.0 - FR 10.2.9 -->

In a trend graph, up to now, a drop-down list in the top-right corner allowed you to select one of the available trend prediction types or “Auto”. This drop-down list has now been removed. Instead, you can now right-click the graph and select one of the available trend prediction types or “Auto” from the context menu.

#### Browser callbacks can now open EPM objects via SystemName or SystemType \[ID_33963\]

<!-- MR 10.3.0 - FR 10.2.9 -->

When an embedded web page is displayed in Cube, it is possible to make a callback from the web page into Cube and, for example, open an element, service, view or CPE card.

The existing JavaScript web browser callbacks for browser shapes in Visual Overview have now been extended to allow opening an EPM card in Cube via an object’s SystemName or SystemType using the following method:

```txt
NavigateCPEByName(string systemType, string systemName);
```

Example in HTML:

```html
<a href='javascript:window.external.NavigateCPEByName("Region","California");'>Open Region California</a>
```

#### Automation app: Casing of a script name can now be changed [ID_33988]

<!-- MR 10.3.0 - FR 10.2.9 -->

In the Automation app, it is now possible to change the casing of a script name.

Also, if you change the casing of a script name that was selected, it will remain selected.

#### Visual Overview - Conditional shape manipulation: Using statistics in the condition when the shape is linked to an EPM object [ID_34026]

<!-- MR 10.3.0 - FR 10.2.9 -->

When applying conditional shape manipulation actions to a shape, up to now, it was only possible to use statistics in the condition if the shape was linked to an element, a service or a view. From now on, you can also use statistics in the condition when the shape is linked to an EPM object.

Example in which both the SystemName and the SystemType are linked:

```txt
<A>-A|SystemType= Cable;SystemName=SF Cable1|#TotalAlarms|>0
```

Supported statistics:

- #TotalAlarms
- #CriticalAlarms
- #MajorAlarms
- #MinorAlarms
- #WarningAlarms
- #NormalAlarms
- #TimeoutAlarms
- #NoticeAlarms
- #ErrorAlarms

Supported operators:

- =
- !=
- \>
- \>=
- \<
- \<=

## Changes

### Enhancements

#### Desktop app: Enhanced host detection \[ID_31829\]

<!-- MR 10.3.0 - FR 10.2.2 -->

In the DataMiner Cube desktop app, a number of enhancements have been made with regard to host detection.

#### Desktop app start window now has a look and feel that is identical to that of the other Cube apps \[ID_32161\]

<!-- MR 10.3.0 - FR 10.2.3 -->

The start window of the DataMiner Cube desktop app has now been adapted so that its overall look and feel is identical to that of the other Cube apps.

#### Desktop app - Start window: Performance enhancements \[ID_33384\]

<!-- MR 10.3.0 - FR 10.2.7 -->

Because of a number of enhancements, overall performance has increased when opening the start window of the DataMiner Cube desktop app from the system tray icon.

#### Alarm Console: Pencil icon now identical to that used in Data Display tables \[ID_33442\]

<!-- MR 10.3.0 - FR 10.2.7 -->

The pencil icon used in the Alarm Console is now identical to that used in Data Display tables.

#### Alarm Console: 'Add to incident' menu option no longer available when right-clicking alarms that cannot be added to an incident \[ID_33591\]

<!-- MR 10.3.0 - FR 10.2.8 -->

From now on, the “Add to incident” menu option will no longer be available when you right-click an alarm that cannot be added to an incident:

- Active alarms with severity “normal” (i.e. clearable alarms that have not been cleared yet)
- Alarms with a source other “DataMiner System” (e.g. correlation alarms)
- Alarms associated with DataMiner itself
- Notices, errors, information events and suggestion events

#### Start window enhancements [ID_34033]

<!-- MR 10.3.0 - FR 10.2.9 -->

A number of enhancements have been made to the DataMiner Cube start window:

- When you hover over a cluster tile, a tooltip will now appear, showing the cluster name, the cluster alias, the hostname of the agent and the last-known server version (if any). The latter will be updated when you connect to the cluster in question and when an update occurs in the background.

    > [!NOTE]
    > Cluster tiles will no longer display the hostname of the agent if it is identical to the cluster alias.

- When using the search box to filter the tiles, the last-known server version will now also be checked. This will allow users to search for clusters with a specific server version.

- When you check for updates (by clicking the cogwheel icon in the bottom-right corner and selecting *Check for updates*), the last-known server version will now be taken into account to avoid having to contact every configured cluster. If a DataMiner Agent has been upgraded since the last background update, the new client version will be downloaded from the agent the first time you connect to it or from the cloud during the next background update (if that version is newer that the current version).

    > [!NOTE]
    >
    > - If you hold the SHIFT key when clicking *Check for updates*, a full update will start. Depending on the number of clusters in your configuration, this can take some time.
    > - An update triggered by the *Update DataMiner Cube_ [userID]* task in Windows Task Scheduler will always be a full update.

- When the start window application is downloaded from a DataMiner Agent, the cluster is automatically configured. Up to now, if it was possible to reach the agent via HTTPS within 2 seconds, the cluster was configured as "HTTPS only". However, in some cases, 2 seconds was too short, resulting in HTTPS agents being configured as "HTTP or HTTPS". From now on, the start window application will wait up to 5 seconds.

- When you add a new cluster, it will now always be added to the group containing the currently selected cluster.
- The maximum size of the daily log file has been increased from 1 MB to 100 MB.

#### Resources app: Deleting a function resource that was used by a canceled booking [ID_34159] [ID_34186]

<!-- MR 10.3.0 - FR 10.2.10 -->

From now on, it will be possible to delete a function resource that was used by a canceled booking.

#### Trending: Enhanced performance when requesting real-time trend data [ID_34171]

<!-- MR 10.3.0 - FR 10.2.10 -->

On systems that store real-time trend data for more than a week, from now on, DataMiner Cube will no longer request all available real-time trend data at once. Instead, it will request data for the past week and only request more data when needed.

### Fixes

#### Visual Overview: Problem when navigating inside EPM cards \[ID_32288\]

<!-- MR 10.3.0 - FR 10.2.3 -->

When working inside an EPM card, in some cases, it would no longer be possible to navigate to a data page or a subpage.

#### Visual Overview: Card buttons in an EPM card would no longer work when the Topology sidebar was selected \[ID_32372\]

<!-- MR 10.3.0 - FR 10.2.3 -->

When an EPM card was opened from a visual overview, and the Topology tab was selected in the sidebar, a number of buttons inside that EPM card would no longer work.

#### Properties not shown in the Surveyor \[ID_32429\]

<!-- MR 10.3.0 - FR 10.2.3 -->

In some cases, properties with the “Display this property in the Surveyor” option enabled would incorrectly not be displayed in the Surveyor.

From now on, when you create a new property and enable its “Display this property in the Surveyor” option, it will immediately show up in the Surveyor, and when you enable that option for an existing property, the property will show up in the Surveyor the first time its value is updated or the next time the user logs in.

When users enable the option for an existing property, a tooltip will now inform them that the value will only appear after logging off and logging in again.

#### Alarm templates: Anomaly detection alarms would incorrectly disappear after a DataMiner restart \[ID_33278\]

<!-- MR 10.3.0 - FR 10.2.6 -->

From DataMiner 10.0.3 onwards, you can configure an alarm template so that alarms are generated instead of suggestion events when anomalies are detected for specific parameters.

Up to now, these anomaly detection alarms would incorrectly disappear from the Alarm Console after a DataMiner restart.

#### Desktop app: Problem when creating a new group in the start window \[ID_33300\]

<!-- MR 10.3.0 - FR 10.2.6 -->

In some rare cases, an error could occur when you created a new group in the start window of the DataMiner Cube desktop app.

Also, the name of a group could get lost when you deleted the first agent/cluster in that group.

#### Visual Overview: Session variables of Resource Manager component would incorrectly be set to NULL when cleared \[ID_33527\]

<!-- MR 10.3.0 - FR 10.2.7 -->

When the following session variables of an embedded Resource Manager component were cleared, up to now, they would incorrectly be set to NULL. From now on, they will be set to an empty value instead.

- ResourcesInSelectedReservation
- SelectedOccurrence
- SelectedPool
- SelectedReservation
- SelectedReservationDefinition
- SelectedResource
- SelectedSession
- TimerangeOfSelectedReservation

#### Resources app: Empty Occupancy tab \[ID_33540\]

<!-- MR 10.3.0 - FR 10.2.8 -->

The first time you clicked the *Occupancy* tab after opening the *Resources* app, in some rare cases, that tab would incorrectly be empty.

#### Profiles app: Selected list items not visible on the UI would incorrectly not be validated after being edited \[ID_33753\]

<!-- MR 10.3.0 - FR 10.2.9 -->

When, in the Profiles app, you edited a profile definition, a profile instance, a profile parameter or a service definition, the change would incorrectly not be validated if the item in question was not visible in the list.

#### Profiles app: No validation errors were displayed when no discrete values had been added yet for a profile parameter of type discrete \[ID_33756\]

<!-- MR 10.3.0 - FR 10.2.9 -->

When an error occurred while configuring a profile parameter of type “discrete”, up to now, that error would not be displayed on the UI when no discrete values had been added yet.

#### Resources app: Warning messages were incorrectly shown in the footer when resource manager configuration requests returned error trace data \[ID_33780\]

<!-- MR 10.3.0 - FR 10.2.9 -->

When you open the *Resources* app, a warning will be shown in the footer when error trace data was found when fetching resource manager data from the server. Up to now, such a warning would incorrectly also be shown when resource manager configuration requests returned error trace data.

#### Resources app: Updating a session variable in a Resource Manager component would incorrectly cause that same session variable to be updated in the Occupancy tab of the Resources app \[ID_33800\]

<!-- MR 10.3.0 - FR 10.2.9 -->

When a session variable (e.g. YAxisResources) was updated in an embedded Resource Manager component, in some cases, that same session variable would also incorrectly be updated in the *Occupancy* tab of the Resources app.

#### Problem with validation of properties and actions in service definitions [ID_34023]

<!-- MR 10.3.0 - FR 10.2.9 -->

When properties or actions of a service definition were configured, it could occur that validation did not happen correctly so that an incorrect configuration could be saved, resulting in exceptions in the server logging and problems in Cube.

The validation will now ensure that no empty names or property names that are incompatible with Elasticsearch can be saved. If there is an error in a service definition, the *Modified* label will change color. Hovering the mouse pointer over the entry with the label will show the first error in the service definition.

#### Clicking the 'Close' button of one of multiple open error message boxes would incorrectly always close the last box that had been opened [ID_34173]

<!-- MR 10.3.0 - FR 10.2.10 -->

When multiple error messages boxes were being displayed, clicking the *Close* button on any of those boxes would incorrectly always close the last box that had been opened. All other boxes would stay open and could only be closed by clicking the X in the top-right corner.

#### Alarm Console: Problem when clearing alarm groups [ID_34196]

<!-- MR 10.3.0 - FR 10.2.10 -->

Alarm groups would not get cleared automatically when the *AutoClear* option was set to false.

Also, in some cases, after clearing an alarm group, a clearable version of that alarm group would incorrectly remain visible in the Alarm Console, even when the *AutoClear* option was set to true.
