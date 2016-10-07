---
author: jpjofre
description: 
external help file: Microsoft.PowerShell.Commands.Management.dll-Help.xml
keywords: powershell, cmdlet
manager: carolz
ms.date: 2016-09-20
ms.prod: powershell
ms.technology: powershell
ms.topic: reference
online version: http://go.microsoft.com/fwlink/?LinkID=113418
schema: 2.0.0
title: Test-Path
---

# Test-Path
## SYNOPSIS
Determines whether all elements of a path exist.
## SYNTAX

### Path (Default)
```
Test-Path [-Path] <String[]> [-Filter <String>] [-Include <String[]>] [-Exclude <String[]>]
 [-PathType <TestPathType>] [-IsValid] [-Credential <PSCredential>] [-UseTransaction] [-OlderThan <DateTime>]
 [-NewerThan <DateTime>] [<CommonParameters>]
```

### LiteralPath
```
Test-Path -LiteralPath <String[]> [-Filter <String>] [-Include <String[]>] [-Exclude <String[]>]
 [-PathType <TestPathType>] [-IsValid] [-Credential <PSCredential>] [-UseTransaction] [-OlderThan <DateTime>]
 [-NewerThan <DateTime>] [<CommonParameters>]
```

## DESCRIPTION
The Test-Path cmdlet determines whether all elements of the path exist.
It returns TRUE ($true) if all elements exist and FALSE ($false) if any are missing.
It can also tell whether the path syntax is valid and whether the path leads to a container or a terminal (leaf) element.
## EXAMPLES

### -------------------------- EXAMPLE 1 --------------------------
```
PS C:\>test-path -path "C:\Documents and Settings\NicoleH"
```

This command tells whether all elements in the path exist, that is, the C: directory, the Documents and Settings directory, and the NicoleH directory.
If any are missing, the cmdlet returns FALSE.
Otherwise, it returns TRUE.
### -------------------------- EXAMPLE 2 --------------------------
```
PS C:\>test-path -path $profile
PS C:\>test-path -path $profile -IsValid
```

These commands test the path to the Windows PowerShell profile.

The first command determines whether all elements in the path exist.
The second command determines whether the syntax of the path is correct.
In this case, the path is FALSE, but the syntax is correct (TRUE).
These commands use $profile, the automatic variable that points to the location for the profile, even if the profile does not exist.

For more information about automatic variables, see about_Automatic_Variables.
### -------------------------- EXAMPLE 3 --------------------------
```
PS C:\>test-path -path "C:\CAD\Commercial Buildings\*" -exclude *.dwg
```

This command tells whether there are any files in the Commercial Buildings directory other than .dwg files.

The command uses the Path parameter to specify the path.
Because it includes a space, the path is enclosed in quotes.
The asterisk at the end of the path indicates the contents of the Commercial Building directory.
(With long paths, like this one, type the first few letters of the path, and then use the TAB key to complete the path.)

The command uses the Exclude parameter to specify files that will be omitted from the evaluation.

In this case, because the directory contains only .dwg files, the result is FALSE.
### -------------------------- EXAMPLE 4 --------------------------
```
PS C:\>test-path -path $profile -pathtype leaf
```

This command tells whether the path stored in the $profile variable leads to a file.
In this case, because the Windows PowerShell profile is a .ps1 file, the cmdlet returns TRUE.
### -------------------------- EXAMPLE 5 --------------------------
```
PS C:\>test-path -path HKLM:\Software\Microsoft\PowerShell\1\ShellIds\Microsoft.PowerShell
TRUE
PS C:\>test-path -path HKLM:\Software\Microsoft\PowerShell\1\ShellIds\Microsoft.PowerShell\ExecutionPolicy
FALSE
```

These commands use the Test-Path cmdlet with the Windows PowerShell registry provider.

The first command tests whether the registry path to the Microsoft.PowerShell registry key is correct on the system.
If Windows PowerShell is installed correctly, the cmdlet returns TRUE.

Test-Path does not work correctly with all Windows PowerShell providers.
For example, you can use Test-Path to test the path to a registry key, but if you use it to test the path to a registry entry, it always returns FALSE, even if the registry entry is present.
## PARAMETERS

### -OlderThan
Returns "True" when the LastWriteTime value of a file is less than the specified date. Otherwise, it returns "False". Enter a DateTime object, such as one that the Get-Date cmdlet returns, or a string that can be converted to a DateTime object, such as "August 10, 2011 2:00 PM".

OlderThan is a dynamic parameter that works only on file system paths. It was introduced in Windows PowerShell 3.0.```yaml
Type: DateTime
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NewerThan
Returns "True" when the LastWriteTime value of a file is greater than the specified date. Otherwise, it returns "False". Enter a DateTime object, such as one that the Get-Date cmdlet returns, or a string that can be converted to a DateTime object, such as "August 10, 2011 2:00 PM".

NewerThan is a dynamic parameter that works only on file system paths. It was introduced in Windows PowerShell 3.0.```yaml
Type: DateTime
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
Specifies a user account that has permission to perform this action.
The default is the current user.

Type a user name, such as "User01" or "Domain01\User01".
Or, enter a PSCredential object, such as one generated by the Get-Credential cmdlet.
If you type a user name, you will be prompted for a password.

This parameter is not supported by any providers installed with Windows PowerShell.

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: Current user
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Exclude
Omits the specified items.
The value of this parameter qualifies the Path parameter.
Enter a path element or pattern, such as "*.txt".
Wildcards are permitted.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Filter
Specifies a filter in the provider's format or language.
The value of this parameter qualifies the Path parameter.
The syntax of the filter, including the use of wildcards, depends on the provider.
Filters are more efficient than other parameters, because the provider applies them when retrieving the objects rather than having Windows PowerShell filter the objects after they are retrieved.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Include
Tests only the specified paths.
The value of this parameter qualifies the Path parameter.
Enter a path element or pattern, such as "*.txt".
Wildcards are permitted.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -IsValid
Determines whether the syntax of the path is correct, regardless of whether the elements of the path exist.
This parameter returns TRUE if the path syntax is valid and FALSE if it is not.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -LiteralPath
Specifies a path to be tested.
Unlike Path, the value of the LiteralPath parameter is used exactly as it is typed.
No characters are interpreted as wildcards.
If the path includes escape characters, enclose it in single quotation marks.
Single quotation marks tell Windows PowerShell not to interpret any characters as escape sequences.

```yaml
Type: String[]
Parameter Sets: LiteralPath
Aliases: PSPath

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Path
Specifies a path to be tested.
Wildcards are permitted.
If the path includes spaces, enclose it in quotation marks.
The parameter name ("Path") is optional.

```yaml
Type: String[]
Parameter Sets: Path
Aliases: 

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### -PathType
Tells whether the final element in the path is of a particular type.
This parameter returns TRUE if the element is of the specified type and FALSE if it is not.

Valid values are:

- Container: An element that contains other elements, such as a directory or registry key.
- Leaf: An element that does not contain other elements, such as a file.
- Any: Either a container or a leaf. Tells whether the final element in the path is of a particular type. Returns TRUE if the element is of the specified type and FALSE if it is not.

```yaml
Type: TestPathType
Parameter Sets: (All)
Aliases: Type

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseTransaction
Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: usetx

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).
## INPUTS

### System.String
You can pipe a string that contains a path (but not a literal path) to Test-Path.
## OUTPUTS

### System.Boolean
The cmdlet returns "True" when the path exists and "False" when it does not.
## NOTES
* The cmdlets that contain the Path noun (the Path cmdlets) manipulate path names and return the names in a concise format that all Windows PowerShell providers can interpret. They are designed for use in programs and scripts where you want to display all or part of a path name in a particular format. Use them like you would use Dirname, Normpath, Realpath, Join, or other path manipulators.

  You can use the Path cmdlets with several providers, including the FileSystem, Registry, and Certificate providers.

  The Test-Path cmdlet is designed to work with the data exposed by any provider.
To list the providers available in your session, type "Get-PSProvider".
For more information, see about_Providers.

*
## RELATED LINKS

[Convert-Path](.\Convert-Path.md)

[Join-Path](.\Join-Path.md)

[Resolve-Path](.\Resolve-Path.md)

[Split-Path](.\Split-Path.md)

[about_Providers](..\Microsoft.PowerShell.Core\About\about_Providers.md)

