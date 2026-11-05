---
description: Builds an assignment for a deployment.
noIndex: true
noRobotsIndex: true
---

# New-PmpcDeploymentAssignment

## Synopsis

Builds an assignment for a deployment.

## Syntax

### Group (Default)

```powershell
New-PmpcDeploymentAssignment [-GroupId] <String> [-Intent] <InstallationIntent>
  [<CommonParameters>]
```

### Target

```powershell
New-PmpcDeploymentAssignment [-Intent] <InstallationIntent>
  -TargetType <AssignmentTargetType> [<CommonParameters>]
```

## Description

Creates the assignment object that New-PmpcDeployment and Set-PmpcDeployment accept, pairing an installation intent with a target.

By default it targets an Entra ID group, given by -GroupId, which is how assignments were always built. To target All Users or All Devices, or to create an install-app/update-only deployment assigned to nobody, pass -TargetType instead of -GroupId.

It exists so assignments can be built at the prompt without constructing a generated-client type by hand.

## Parameters

### -GroupId

Entra ID group the application is assigned to. Targets a group; omit it and pass -TargetType for the other targets.

| Attribute      | Value                          |
| -------------- | ------------------------------ |
| Type           | `System.String`                |
| Required       | True                           |
| Position       | 0                              |
| Pipeline input | True (ByValue, ByPropertyName) |
| Aliases        | None                           |
| Parameter sets | Group                          |

### -Intent

Whether the assignment installs the application or merely makes it available.

| Attribute       | Value                                                                                                                      |
| --------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Type            | `InstallationIntent`                                                                                                       |
| Required        | True                                                                                                                       |
| Position        | 1                                                                                                                          |
| Pipeline input  | True (ByPropertyName)                                                                                                      |
| Aliases         | None                                                                                                                       |
| Accepted values | Unknown, UpdateOnly, Available, Required, Uninstall, AvailableWithoutEnrollment, NoAssignmentsInstall, NoAssignmentsUpdate |
| Parameter sets  | All                                                                                                                        |

### -TargetType

The assignment target when it is not a group: AllUsers, AllDevices, or NotSet for a no-assignment marker. Takes no group id.

| Attribute       | Value                               |
| --------------- | ----------------------------------- |
| Type            | `AssignmentTargetType`              |
| Required        | True                                |
| Position        | Named                               |
| Pipeline input  | False                               |
| Aliases         | None                                |
| Accepted values | AllUsers, AllDevices, Group, NotSet |
| Parameter sets  | Target                              |

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutBuffer, -OutVariable, -PipelineVariable, -ProgressAction, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about\_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### System.String

The group ID, by value or by the GroupId property.

## Outputs

### CreateDeploymentAssignmentRequest

The assignment object.

## Examples

### Example 1: Build a required assignment

```powershell
New-PmpcDeploymentAssignment -GroupId $groupId -Intent Required
```

Creates an assignment that installs the application on the group's devices.

### Example 2: Build several assignments

```powershell
$assignments = @(
  New-PmpcDeploymentAssignment -GroupId $pilotGroup -Intent Required
  New-PmpcDeploymentAssignment -GroupId $allUsers -Intent Available
)
New-PmpcDeployment -ProductId $productId -OsType Windows -Assignment $assignments
```

Makes the application required for a pilot group and available to everyone else.

### Example 3: Assign to All Devices

```powershell
New-PmpcDeploymentAssignment -TargetType AllDevices -Intent Required
```

Targets every managed device in the tenant, with no group. Use AllUsers for every user.

### Example 4: Create an install-app deployment assigned to nobody

```powershell
New-PmpcDeploymentAssignment -TargetType NotSet -Intent NoAssignmentsInstall
```

Produces the marker the portal writes for an "install app" (or "update only", with NoAssignmentsUpdate) deployment that is assigned to no group.

## Notes

This cmdlet makes no network call and does not require a session.

The -GroupId and -TargetType forms are separate parameter sets: -GroupId targets a group, while -TargetType covers AllUsers, AllDevices, and NotSet (a no-assignment marker) and takes no group.

The no-assignment intents (NoAssignmentsInstall, NoAssignmentsUpdate) require the NotSet target: either omit -TargetType or pass -TargetType NotSet. Pairing a no-assignment intent with an explicit AllUsers, AllDevices, or Group target is rejected by the service with 400 Bad Request naming the field; it is not silently coerced. Passing -TargetType Group is refused locally, before any call, because that set carries no group id.

## Related links

* [New-PmpcDeployment](new-pmpcdeployment.md)
* [Set-PmpcDeployment](set-pmpcdeployment.md)
* PowerShell module

## See also

This cmdlet has no SDK method or REST operation of its own.

* [Cross-reference: cmdlets, SDK methods, and REST operations](../cross-reference.md)
