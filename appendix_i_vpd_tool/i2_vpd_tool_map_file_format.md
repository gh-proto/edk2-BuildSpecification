<!--- @file
  I.2 VPD Tool Map File Format

  Copyright (c) 2008-2017, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

-->

## I.2 VPD Tool Map File Format

#### Summary

The build system will expect the following format in the file generated by an
external tool that processes the VPD PCDs. This format will be used by the
build system to generate header files for the PCD drivers.

#### Prototype

```c
<File>            ::= <AutoGenHeader>
                      [<CommentBlock>]
                      [<PcdEntry>]*
<AutoGenHeading>  ::= "## @file" <EOL> "#" <EOL>
                      "# THIS IS AUTO-GENERATED FILE BY BUILD TOOLS"
                      " AND PLEASE DO NOT MAKE MODIFICATION." <EOL>
                      "#" <EOL>
                      "# This file lists all VPD information for a"
                      " platform collected by build.exe." <EOL>
                      "#" <EOL>
                      "# Copyright (c) 2010, Intel Corporation. All"
                      " rights reserved.<BR>"
                      "# This program and the accompanying materials"
                      "# are licensed and made available under the"
                      " terms and conditions of the BSD License"
                      "# which accompanies this distribution. The"
                      " full text of the license may be found at"
                      "# "
                      "http://opensource.org/licenses/bsd-license.php"
                      <EOL> "#" <EOL>
                      "# THE PROGRAM IS DISTRIBUTED UNDER THE BSD"
                      " LICENSE ON AN \"AS IS\" BASIS,"
                      "# WITHOUT WARRANTIES OR REPRESENTATIONS OF ANY"
                      " KIND, EITHER EXPRESS OR IMPLIED."
<CommentBlock>    ::= ["#" <String> <EOL>]*
<FS>              ::= <Space>* "|" <Space>*
<Space>           ::= 0x20
<PcdEntry>        ::= <PcdName> <FS> <Offset> <FS> <PcdValue> <EOL>
<PcdName>         ::= <TokenSpaceCName> "." <PcdCName>
<TokenSpaceCName> ::= C Variable Name of the Token Space GUID
<PcdCName>        ::= C Variable Name of the PCD
<Offset>          ::= "0x" (a-fA-F0-9){1,8}
<Size>            ::= <Number>
<PcdValue>        ::= if (pcddatumtype == "BOOLEAN"):
                        "BOOLEAN" <FS> <Boolean>
                      elif (pcddatumtype == "UINT8"):
                        "UINT8" <FS> <HexByteZ>
                      elif (pcddatumtype == "UINT16"):
                        "UINT16" <FS> <HexWordZ>
                      elif (pcddatumtype == "UINT32"):
                        "UINT32" <FS> <HexLongZ>
                      elif (pcddatumtype == "UINT64"):
                        "UINT64" <FS> <HexLongLongZ>
                      else:
                        <Size> <FS> <StringData>
<HexByteZ>        ::= "0x"(a-fA-F0-9)(a-fA-F0-9)
<HexWord>         ::= "0x" (a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)
<HexLong>         ::= "0x" (a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)
                           (a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)
<HexLongLong>     ::= "0x" (a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)
                           (a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)
                           (a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)
                           (a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)(a-fA-F0-9)
<Number>          ::= {<HexNumber>} {<NonNegativeInt>}
<Boolean>         ::= {<True>} {<False>}
<True>            ::= {"TRUE"} {"True"} {"true"} {"1"} {"0x1"} {"0x01"}
<False>           ::= {"FALSE"} {"False"} {"false"} {"0"} {"0x0"} {"0x00"}
<HexNumber>       ::= "0x" (a-fA-F0-9){2,16}
<NonNegativeInt>  ::= (0-9)+
<StringData>      ::= {<QString>} {<CArray>}
<QString>         ::= ["L"] <DblQuote> <String> <DblQuote>
<DblQuote>        ::= 0x22
<CArray>          ::= "{" <HexByte> ["," <HexByte>]* "}"
<NList>           ::= <HexByte> ["," <HexByte>]*
```

#### Example

```ini
## @file
#
# THIS IS AUTO-GENERATED FILE BY BPDG TOOLS AND PLEASE DO NOT MAKE MODIFICATION.
#
# This file lists all VPD informations for a platform fixed/adjusted by BPDG tool.
#
# Copyright (c) 2010, Intel Corporation. All rights reserved.<BR>
# This program and the accompanying materials
# are licensed and made available under the terms and conditions of the BSD License
# which accompanies this distribution. The full text of the license may be found at
# http://opensource.org/licenses/bsd-license.php
#
# THE PROGRAM IS DISTRIBUTED UNDER THE BSD LICENSE ON AN "AS IS" BASIS,
# WITHOUT WARRANTIES OR REPRESENTATIONS OF ANY KIND, EITHER EXPRESS OR IMPLIED.
#
gEfiMdeModulePkgTokenSpaceGuid.PcdVideoHorizontalResolution | 0x0 | 4 | 800
gEfiMdeModulePkgTokenSpaceGuid.PcdVideoVerticalResolution | 0x4 | 4 | 600
gEfiMdeModulePkgTokenSpaceGuid.PcdConOutRow | 0x8 | 4 | 25
gEfiMdeModulePkgTokenSpaceGuid.PcdConOutColumn | 0xc | 4 | 80
```