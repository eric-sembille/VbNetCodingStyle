# Contributing to CDS

## Summary
- [Commit message format](#cof)
- [VB.Net coding style](#vbcs)

## <a name="cof"></a> Commit message format
Each commit message consists of a **header** and a **body**.  The header has a special
format that includes a **type**, a **scope** and a **subject**:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
```

The **header** is mandatory and the **scope** of the header is optional.

Any line of the commit message cannot be longer 100 characters! This allows the message to be easier
to read on GitHub as well as in various git tools.

### Type
Must be one of the following:

* **feat**: A new feature
* **fix**: A bug fix
* **docs**: Documentation only changes
* **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing
  semi-colons, etc)
* **refactor**: A code change that neither fixes a bug nor adds a feature
* **perf**: A code change that improves performance
* **test**: Adding missing or correcting existing tests
* **chore**: Changes to the build process or auxiliary tools and libraries such as documentation
  generation

### Subject
The subject contains succinct description of the change:

* use the imperative, present tense: "change" not "changed" nor "changes"
* don't capitalize first letter
* no dot (.) at the end

### Body
Just as in the **subject**, use the imperative, present tense: "change" not "changed" nor "changes".
The body should include the motivation for the change and contrast this with previous behavior.

Reference : [Angular JS](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#commit)

## <a name="vbcf"></a>VB.Net coding style

### Style vocabulary

- **Do** : is one that should always be followed. Always might be a bit too strong of a word.
- **Consider** : guidelines should generally be followed. If you fully understand the meaning behind the guideline and have a good reason to deviate, then do so
- **Avoid** : There could be exception
- **Do Not** : indicates something you should almost never do. Code examples to avoid have an unmistakeable red header.
- **Why ?** gives reasons for following the previous recommendations.

### Class
#### DO Respect the SRP (Single Responsabilty Principle)

#### CONSIDER One class per file

#### CONSIDER limiting to more than 500 lines

#### DO Order elements in a class

1. const
4. attributes
5. construtors
6. finalizers 
7. delegate
8. event
9. property
10. function and subs

Within each of these groups order by access
 - public
 - friend
 - protected friend
 - protected
 - private

Within each of the access groups, order by static, then non-static
 - static
 - non-static

Within each of the static/non-static groups of fields, order by readonly, then non-readonly
 - readonly
 - non-readonly

#### AVOID Class name suffix like helper or manager
> Why ? the class name is generic. It means that the class don't respect SRP

### Functions and subs

#### DO Define small functions

#### CONSIDER limiting to more than 100 lines

#### AVOID Define functions/subs with more than 3 parameters

#### AVOID using out or ref parameters

#### DO NOT pass reference types by reference

```
' Bad
Private Sub MyMethod(ByRef param1 as MyClass)
End Sub
' Good 
Private Sub MyMethod(param1 as MyClass)
End Sub
```

#### DO NOT ByVal keyword when is useless

```
' Bad
Private Sub MyMethod(ByVal param1 as Integer)
End Sub
' Good 
Private Sub MyMethod(param1 as Integer)
End Sub
```

#### DO use the least derived parameter type that provides the functionality required by the member
> Such a method should take IEnumerable as the parameter, not ArrayList or IList, for example

```
' Bad
Private Sub MyMethod(collection as List(Of MyClass))
End Sub
' Good 
Private Sub MyMethod(collection as IEnumerable(Of MyClass))
End Sub
```

#### DO use paranthesis on subs/functions even if there are useless

```
' Bad
MyMethod
' Good 
MyMethod()
```

#### DO Specify access modifier
Bad
```
Sub MySub() 
End
```
Good
```
Private Sub MySub() 
End
```

### Properties
#### AVOID Use property why parameter

#### DO NOT Use parenthesis after property name

Bad
```
Public Property MyProperty() As Integer 
```
Good
```
Public Property MyProperty As Integer 
```

#### DO Use auto property

Bad
```
Private _myProperty As Integer

Public Property MyProperty As Integer 
	Get
		Return _myProperty
	End Get
	Set
        _myProperty = value
	End Set
End Property
```
Good
```
Public Property MyProperty As Integer 
```

#### DO NOT Define setter parameter
Bad
```
Public Property MyProperty As Integer 
	Get
		Return _myProperty
	End Get
	Set(ByVal value As Integer)
        _myProperty = value
	End Set
End Property
```
Good
```
Public Property MyProperty As Integer 
	Get
		Return _myProperty
	End Get
	Set
        _myProperty = value
	End Set
End Property
```

### DO NOT Use write only property
> Perfer use a method

Bad
```
Private _myProperty As Integer

Public Property MyProperty As Integer 
	Set
        _myProperty = value
	End Set
End Property
```
Good
```
Public Sub SetMyProperty(value As Integer)
        _myProperty = value
End Sub
```


### Naming

#### DO Using casing convetion
 - "c" = camelCase
 - "P" = PascalCase
 - "_" = Prefix with _Underscore
 - "x" = Not Applicable.

|  Identifier       |Public |Protected|Internal|Private|Notes
| --------------    |:----: |:-------:|:------:|:-----:|----- 
|Project File       |P      |x        |x       |x      |Match Assembly & Namespace.
|Source File        |P      |x        |x       |x      |Match contained class.
|Other Files        |P      |x        |x       |x      |Apply where possible.
|Namespace          |P      |x        |x       |x      |Partial Project/Assembly match.
|Class or Struct    |P      |P        |P       |P      |Add suffix of subclass.
|Interface          |P      |P        |P       |P      |Prefix with a capital I.
|Generic Class      |P      |P        |P       |P      |Use T or K as Type identifier.
|Method             |P      |P        |P       |P      |Use a Verb or Verb-Object pair.
|Property           |P      |P        |P       |P      |Do not prefix with Get or Set.
|Field              |P      |P        |P       |_c     |Only use Private fields. No Hungarian Notation!
|Constant           |P      |P        |P       |_c     |
|Static Field       |P      |P        |P       |_c     |Only use Private fields.
|Enum               |P      |P        |P       |P      |Options are also PascalCase.
|Delegate           |P      |P        |P       |P      |
|Event              |P      |P        |P       |P      |
|Inline Variable    |x      |x        |x       |c      |Avoid single-character and enumerated names.
|Parameter          |x      |x        |x       |c      |

#### DO Using PascalCasing casing for
 - Classes
 - Methods
 - Properties
 - Constants
 - Statics
 - 
#### DO Using camel casing for
 - Method parameters
 - Inline Variable
 - 
#### DO Using "_" prefix for class attribute

#### DO NOT Using SCREAMING upper case
> Why ?: consistent with the Microsoft's .NET Framework. Caps grap too much attention.

#### DO prefix interfaces with the letter I.  Interface names are noun (phrases) or adjectives.

#### DO NOT use Hungarian notation or any other type identification in identifiers

```
' Bad 
Dim iMyVal as Integer
' Good
Dim myVal as Integer
```

#### AVOID Using abreviation
```
' Bad 
Dim usrGrp as UserGroup
Dim empAssignment As Assignment
' Good
Dim userGroup As UserGroup
Dim employeeAssignment As Assignment
```

### DO Use suffix instead of suffix
```
' Bad 
Dim btnValidation as Buton
Dim tbName As TextBox
' Good
Dim validationButon As Buton
Dim nameTextBox As TextBox
```

#### DO NOT suffix enum names with Enum 

#### DO NOT prefix enum names with E 

### Comments

#### AVOID Commented code

#### AVOID comments in Subs/Functions
Bad
```
' Si la personne est majeure
If personne.Age >= 18
End If 
```
Good
```
If personne.EstMajeur()
End If 
```
  
### Formating

#### DO Ident code

#### DO NOT Use tab

#### DO Invert "If" to reduce nesting

Bad
```
Private MySub()
    If MyCondition
        DoStuff()
    End If
End Sub
```
Good
```
Private MySub()
    If Not MyCondition
        Return
    End If

    DoStuff()
End Sub
```

#### DO NOT region
> Why ? : regions hide code smell. Regions could be replace by methods or new classes
> Except : For copyright and licencing info at the start of file
#### CONSIDER Line max lenght 100

#### AVOID Use line break "_"
> Prefer use new line after keywords or comma
> Exception for interface implementation and event handler

Bad
```
Dim myVal = new MyClass(param1, param2, param3 _
                        ,param4, param5, param6)

If (condition1 AndAlso condition2) _
    OrElse condition3

End If
```
Good
```
Dim myVal = new MyClass(param1,
                        param2,
                        param3,
                        param4,
                        param5,
                        param6)
                        
If (condition1 AndAlso condition2) OrElse 
        condition3

End If                 
           
Public Sub MySub(param as MyClass) _
    Implements IMyInterface.MySub 
End Sub          
   
Public Sub MySub(sender as Object, e EventArgs) _
    Handles MyButton.Click            
End Sub             
                         
```

#### DO NOT Use "Then" statement for If 
> Exception for test if an argument is nothing 

Bad
```
If MyCondition Then DoStuff()

If MyCondition Then
    DoStuff()
End If
```
Good
```
If MyCondition 
    DoStuff()
End If

Sub MySub(arg as Argument)
    If arg is Nothing then throw New ArgumentNullException(nameof(arg))
    ' Do stuff
End Sub

```

#### AVOID Use paranthesis for if condition
Bad
```
If (MyVal = test)
End If
```
Good
```
If MyVal = test
End I
```

#### DO NOT Define type in For Each Statement
Bad
```
For Each myVal as MyType In myCollection
Next 
```
Good
```
For Each myVal In myCollection
Next 
```

#### DO NOT Respect case for keyword and name
Bad
```
dim myVal as integer = 0
do while myval < 10
    myval ++ 
LOOP
```
Good
```
dim myVal as Integer= 0
Do While myVal < 10
    myVal ++ 
Loop
```

#### DO Add space before and after operator

```
'Bad
Dim i=5+3
'Good
Dim i = 5 + 3
```

#### DO Remove and sort imports
> Use command in Visual Studio

#### DO NOT Use "Me" before methods, attributs or properties

### Exceptions

#### DO Test before to avoid exception throwing

```
'Bad
Function Divide(a as Integer, b as Interger) as Decimal
    Try     
        return a / b
    Catch ex As DivideByZeroException
        Return 0
    End Try
End Function
'Good
Function Divide(a as Integer, b as Interger) as Decimal
    if b = 0 then 
        Return 0
    End If
    
    return a / b
End Function
```

#### DO Throw exceptions instead of returning an error code

#### DO End exception class names with the word

#### DO Include three constructors in custom exception classes

#### DO NOT Catch 'Exception' type

#### DO NOT throw new Exception()

#### AVOID Catch exception only for logging purpose

#### DO NOT clear the stack trace when re-throwing an exception

```
'Bad
Try     
    ' Some code that throws an exception
Catch ex As Exception
    ' some code that handles the exception
    throw ex 
End Try
'Good
Try     
    ' Some code that throws an exception
Catch ex As Exception
    ' some code that handles the exception
    throw 
End Try

Try     
    ' Some code that throws an exception
Catch ex As Exception
    ' some code that handles the exception
    throw New Exception("My message",ex)
End Try
```

### Performance

#### DO Use String.Empty instead of ""

#### DO Use EventArgs.Empty instead of New EventArgs()

#### DO Use "Any" function to test if a collection is empty
Bad
```
If MyCollection.Count > 0
End If
```
Good
```
If Not MyCollection.Any()
End If
```

#### DO Use StringBuilder to build large string

### Some References
 - [Framework Design Guidelines](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/)

## Razor VbHtml coding style

## Javascript coding style

## SQL coding style


