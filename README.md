<div align="center">

## NetServerEnum


</div>

### Description

Enumerate all servers in the domain, or specific server types, like SQL Servers, Workstations etc with API.

Using netapi32.dll
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Eugene Zhukovsky](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/eugene-zhukovsky.md)
**Level**          |Intermediate
**User Rating**    |5.0 (15 globes from 3 users)
**Compatibility**  |C\#
**Category**       |[System Services/ Functions](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/system-services-functions__10-23.md)
**World**          |[\.Net \(C\#, VB\.net\)](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/net-c-vb-net.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/eugene-zhukovsky-netserverenum__10-734/archive/master.zip)





### Source Code

<HTML>
<HEAD>
<META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=windows-1252">
<META NAME="Generator" CONTENT="Microsoft Word 97">
<TITLE>//declare the DLL import functions [DllImport("netapi32</TITLE>
</HEAD>
<BODY>
<FONT FACE="Lucida Console" COLOR="#008000"><P>//Coded by Eugene E. Zhukovsky, 8.21.2002</P>
<P>//declare the DLL import functions</FONT><FONT FACE="Lucida Console"> </P>
<P>[DllImport("netapi32.dll",EntryPoint="NetServerEnum")]</P>
<P>&#9;&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">public</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">static</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">extern</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">int</FONT><FONT FACE="Lucida Console"> NetServerEnum( [MarshalAs(UnmanagedType.LPWStr)]</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">string</FONT><FONT FACE="Lucida Console"> servername, </P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">int</FONT><FONT FACE="Lucida Console"> level, </P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">out</FONT><FONT FACE="Lucida Console"> IntPtr bufptr, </P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">int</FONT><FONT FACE="Lucida Console"> prefmaxlen,</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">ref</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">int</FONT><FONT FACE="Lucida Console"> entriesread, </P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">ref</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">int</FONT><FONT FACE="Lucida Console"> totalentries,</P>
<P>&#9;SV_101_TYPES servertype,</P>
<P>&#9;[MarshalAs(UnmanagedType.LPWStr)]</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">string</FONT><FONT FACE="Lucida Console"> domain,</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">int</FONT><FONT FACE="Lucida Console"> resume_handle);</P>
</FONT><FONT SIZE=2><P> </P>
</FONT><FONT FACE="Lucida Console"><P>[DllImport("netapi32.dll",EntryPoint="NetApiBufferFree")]</P>
</FONT><FONT FACE="Lucida Console" COLOR="#0000ff"><P>public</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">static</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">extern</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">int</FONT><FONT FACE="Lucida Console"> NetApiBufferFree(IntPtr buffer);</P>
</FONT><FONT SIZE=2>
</FONT><FONT FACE="Lucida Console" COLOR="#008000"><P>//declare the structures to hold info</P>
</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">
<P>public</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">enum</FONT><FONT FACE="Lucida Console"> SV_101_TYPES:</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">uint</P>
</FONT><FONT FACE="Lucida Console"><P>{</P>
<P>&#9;SV_TYPE_WORKSTATION    = 0x00000001,</P>
<P>&#9;SV_TYPE_SERVER      = 0x00000002,</P>
<P>&#9;SV_TYPE_SQLSERVER     = 0x00000004,</P>
<P>&#9;SV_TYPE_DOMAIN_CTRL    = 0x00000008,</P>
<P>&#9;SV_TYPE_DOMAIN_BAKCTRL  = 0x00000010,</P>
<P>&#9;SV_TYPE_TIME_SOURCE    = 0x00000020,</P>
<P>&#9;SV_TYPE_AFP        = 0x00000040,</P>
<P>&#9;SV_TYPE_NOVELL      = 0x00000080,</P>
<P>&#9;SV_TYPE_DOMAIN_MEMBER   = 0x00000100,</P>
<P>&#9;SV_TYPE_PRINTQ_SERVER   = 0x00000200,</P>
<P>&#9;SV_TYPE_DIALIN_SERVER   = 0x00000400,</P>
<P>&#9;SV_TYPE_XENIX_SERVER   = 0x00000800,</P>
<P>&#9;SV_TYPE_SERVER_UNIX    = SV_TYPE_XENIX_SERVER,</P>
<P>&#9;SV_TYPE_NT        = 0x00001000,</P>
<P>&#9;SV_TYPE_WFW        = 0x00002000,</P>
<P>&#9;SV_TYPE_SERVER_MFPN    = 0x00004000,</P>
<P>&#9;SV_TYPE_SERVER_NT     = 0x00008000,</P>
<P>&#9;SV_TYPE_POTENTIAL_BROWSER = 0x00010000,</P>
<P>&#9;SV_TYPE_BACKUP_BROWSER  = 0x00020000,</P>
<P>&#9;SV_TYPE_MASTER_BROWSER  = 0x00040000,</P>
<P>&#9;SV_TYPE_DOMAIN_MASTER   = 0x00080000,</P>
<P>&#9;SV_TYPE_SERVER_OSF    = 0x00100000,</P>
<P>&#9;SV_TYPE_SERVER_VMS    = 0x00200000,</P><DIR>
<DIR>
<P>SV_TYPE_WINDOWS      = 0x00400000,&#9;&#9; SV_TYPE_DFS        = 0x00800000,&#9;&#9; SV_TYPE_CLUSTER_NT    = 0x01000000,&#9;&#9; SV_TYPE_TERMINALSERVER  = 0x02000000,&#9;&#9; SV_TYPE_CLUSTER_VS_NT   = 0x04000000,&#9;&#9; SV_TYPE_DCE        = 0x10000000,&#9;&#9; SV_TYPE_ALTERNATE_XPORT  = 0x20000000,&#9;&#9; SV_TYPE_LOCAL_LIST_ONLY  = 0x40000000,&#9;&#9; SV_TYPE_DOMAIN_ENUM    = 0x80000000,</P></DIR>
</DIR>
<P>&#9;SV_TYPE_ALL        = 0xFFFFFFFF </P>
<P>}</P>
<P>[StructLayout(LayoutKind.Sequential)]</P>
</FONT><FONT FACE="Lucida Console" COLOR="#0000ff"><P>public</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">struct</FONT><FONT FACE="Lucida Console"> SERVER_INFO_101</P>
<P>{</P>
<P>&#9;[MarshalAs(System.Runtime.InteropServices.UnmanagedType.U4)]&#9;&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">public</FONT><FONT FACE="Lucida Console"> UInt32&#9;sv101_platform_id;</P>
<P>&#9;[MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPWStr)]&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">public</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">string</FONT><FONT FACE="Lucida Console">  sv101_name;</P>
<P>&#9;[MarshalAs(System.Runtime.InteropServices.UnmanagedType.U4)]&#9;&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">public</FONT><FONT FACE="Lucida Console"> UInt32&#9;sv101_version_major;</P>
<P>&#9;[MarshalAs(System.Runtime.InteropServices.UnmanagedType.U4)]&#9;&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">public</FONT><FONT FACE="Lucida Console"> UInt32&#9;sv101_version_minor;</P>
<P>&#9;[MarshalAs(System.Runtime.InteropServices.UnmanagedType.U4)]&#9;&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">public</FONT><FONT FACE="Lucida Console"> UInt32&#9;sv101_type;</P>
<P>&#9;[MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPWStr)]&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">public</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">string</FONT><FONT FACE="Lucida Console">  sv101_comment;</P>
<P>&#9;}</P>
</FONT><FONT SIZE=2>
</FONT><FONT FACE="Lucida Console" COLOR="#0000ff"><P>public</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">enum</FONT><FONT FACE="Lucida Console"> PLATFORM_ID</P>
<P>{</P>
<P>&#9;PLATFORM_ID_DOS = 300,</P>
<P>&#9;PLATFORM_ID_OS2 = 400,</P>
<P>&#9;PLATFORM_ID_NT = 500,</P>
<P>&#9;PLATFORM_ID_OSF = 600,</P>
<P>&#9;PLATFORM_ID_VMS = 700</P>
<P>}</P>
</FONT><FONT SIZE=2><P>&nbsp;</P>
</FONT><FONT FACE="Lucida Console" COLOR="#008000"><P>//now let's do it!</P>
</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">
<P>public</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">static</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">void</FONT><FONT FACE="Lucida Console"> doit()</P>
<P>{</P>
<P>&#9;SERVER_INFO_101 si;</P>
<P>&#9;IntPtr ppSVINFO = </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">new</FONT><FONT FACE="Lucida Console"> IntPtr();</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">int</FONT><FONT FACE="Lucida Console"> etriesread = 0;</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">int</FONT><FONT FACE="Lucida Console"> totalentries = 0;</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">try</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;{</P>
<P>&#9;&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">if</FONT><FONT FACE="Lucida Console">(NetServerEnum(</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">null</FONT><FONT FACE="Lucida Console">, </P>
<P>&#9;&#9;&#9;&#9;101, </P>
<P>&#9;&#9;&#9;&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">out</FONT><FONT FACE="Lucida Console"> ppSVINFO, </P>
<P>&#9;&#9;&#9;&#9;-1, </P>
<P>&#9;&#9;&#9;&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">ref</FONT><FONT FACE="Lucida Console"> etriesread, </P>
<P>&#9;&#9;&#9;&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">ref</FONT><FONT FACE="Lucida Console"> totalentries, </P>
<P>&#9;&#9;&#9;&#9;SV_101_TYPES.SV_TYPE_ALL, </P>
<P>&#9;&#9;&#9;&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">null</FONT><FONT FACE="Lucida Console">,</P>
<P>&#9;&#9;&#9;&#9;0) == 0 )</P>
<P>&#9;&#9;{</P>
<P>&#9;&#9;&#9;Int32 ptr = ppSVINFO.ToInt32();</P>
<P>&#9;&#9;&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">for</FONT><FONT FACE="Lucida Console">(</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">int</FONT><FONT FACE="Lucida Console"> i = 0; i &lt; etriesread; i++)</P>
<P>&#9;&#9;&#9;{</P>
<P>&#9;&#9;&#9;&#9;si = (SERVER_INFO_101)Marshal.PtrToStructure( </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">new</FONT><FONT FACE="Lucida Console"> IntPtr(ptr), </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">typeof</FONT><FONT FACE="Lucida Console">(SERVER_INFO_101) );</P>
<P>&#9;&#9;&#9;&#9;&#9;</P>
<P>&#9;&#9;&#9;&#9;ptr += Marshal.SizeOf( si );</P>
<P>&#9;&#9;&#9;&#9;}</P>
<P>&#9;&#9;}</P>
<P>&#9;&#9;NetApiBufferFree(ppSVINFO);</P>
<P>&#9;}</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">catch</FONT><FONT FACE="Lucida Console">(Exception e)</P>
<P>&#9;{</P>
<P>&#9;}</P>
<P>}</P>
</FONT><FONT SIZE=2>
</FONT><FONT FACE="Lucida Console" COLOR="#008000"><P>//here's some possible error codes</P>
</FONT><FONT FACE="Lucida Console" COLOR="#0000ff">
<P>public</FONT><FONT FACE="Lucida Console"> </FONT><FONT FACE="Lucida Console" COLOR="#0000ff">enum</FONT><FONT FACE="Lucida Console"> NERR</P>
<P>{</P>
<P>&#9;NERR_Success&#9;= 0,   </FONT><FONT FACE="Lucida Console" COLOR="#008000">/* Success */</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;ERROR_MORE_DATA = 234,  </FONT><FONT FACE="Lucida Console" COLOR="#008000">// dderror</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;ERROR_NO_BROWSER_SERVERS_FOUND = 6118,</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> The system call level is not correct.</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;/summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;ERROR_INVALID_LEVEL&#9;= 124,</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> Access is denied.</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;/summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;ERROR_ACCESS_DENIED&#9;= 5,</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> The parameter is incorrect.</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;/summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;ERROR_INVALID_PARAMETER&#9;= 87,</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> Not enough storage to process this command.</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;/summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;ERROR_NOT_ENOUGH_MEMORY&#9;= 8,</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> The network is busy.</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;/summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;ERROR_NETWORK_BUSY&#9;= 54,</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> The network path was not found.</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;/summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;ERROR_BAD_NETPATH&#9;= 53,</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> The network is not present or not started.</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;/summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;ERROR_NO_NETWORK  = 1222,</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> Handle is in an invalid state.</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;/summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;ERROR_INVALID_HANDLE_STATE  = 1609,</P>
<P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> An extended error has occurred.</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;</FONT><FONT FACE="Lucida Console" COLOR="#808080">///</FONT><FONT FACE="Lucida Console" COLOR="#008000"> </FONT><FONT FACE="Lucida Console" COLOR="#808080">&lt;/summary&gt;</P>
</FONT><FONT FACE="Lucida Console"><P>&#9;ERROR_EXTENDED_ERROR   = 1208</P>
<P>}</P></FONT></BODY>
</HTML>

