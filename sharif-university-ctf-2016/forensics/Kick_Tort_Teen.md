# Kick Tort Teen

## Task

Anagram, anyone?

## Solution

We are given an xls document containing numbers.
If we unzip it, we can see that there are VBA macros.

```
mac:xl rainbowlyte$ ls -la
total 88
drwxr-xr-x@  8 rainbowlyte  wheel    272 Feb  7 17:11 .
drwxrwxrwt  15 root    wheel    510 Feb  7 17:11 ..
drwxr-xr-x@  3 rainbowlyte  wheel    102 Feb  7 17:11 _rels
-rw-r--r--@  1 rainbowlyte  wheel  16372 Jan  1  1980 styles.xml
drwxr-xr-x@  3 rainbowlyte  wheel    102 Feb  7 17:11 theme
-rw-r--r--@  1 rainbowlyte  wheel  22528 Jan  1  1980 vbaProject.bin
-rw-r--r--@  1 rainbowlyte  wheel    641 Jan  1  1980 workbook.xml
drwxr-xr-x@  3 rainbowlyte  wheel    102 Feb  7 17:11 worksheets
```

We used `olevba` to extract the macro.

```vb
VBA MACRO Module1.bas
in file: xl/vbaProject.bin - OLE stream: u'VBA/Module1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Function FileExists(ByVal FileToTest As String) As Boolean
   FileExists = (Dir(FileToTest) <> "")
End Function
Sub DeleteFile(ByVal FileToDelete As String)
   If FileExists(FileToDelete) Then 'See above
      SetAttr FileToDelete, vbNormal
      Kill FileToDelete
   End If
End Sub
Sub DoIt()
    Dim filename As String
    filename = Environ("USERPROFILE") & "\fileXYZ.data"
    DeleteFile (filename)

    Open filename For Binary Lock Read Write As #2
    For i = 1 To 14747
        For j = 1 To 23
            Put #2, , CByte((Cells(i, j).Value - 78) / 3)
        Next
    Next

    Put #2, , CByte(98)
    Put #2, , CByte(13)
    Put #2, , CByte(0)
    Put #2, , CByte(73)
    Put #2, , CByte(19)
    Put #2, , CByte(0)
    Put #2, , CByte(94)
    Put #2, , CByte(188)
    Put #2, , CByte(0)
    Put #2, , CByte(0)
    Put #2, , CByte(0)

    Close #2
End Sub
```

The interesting part is

```
Open filename For Binary Lock Read Write As #2
For i = 1 To 14747
    For j = 1 To 23
        Put #2, , CByte((Cells(i, j).Value - 78) / 3)
    Next
Next
```

We used the corresponding python code to process the numbers in the xls document.

```python
numbers = []
s = ''

with open('numbers', 'r') as f:
	for line in f.readlines():
		l = [int(i) for i in line.split()]
		numbers.append(l)

		for i in numbers:
			for j in i:
				s += chr((j-78) / 3)

with open('exe', 'w') as f:
	f.write(s)
```

The file `exe` is an executable that contains the flag.

```bash
rainbowlyte@ns38534:/tmp$ file exe
exe: ELF 64-bit LSB executable, x86-64, version 1 (GNU/Linux), statically linked, stripped
rainbowlyte@ns38534:/tmp$ chmod +x exe
rainbowlyte@ns38534:/tmp$ ./exe
SharifCTF{5bd74def27ce149fe1b63f2aa92331ab}
```

