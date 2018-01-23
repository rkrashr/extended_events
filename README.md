# extended_events

python.exe.config
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.1" />
    </startup>
    <appSettings>
      <!-- Enables support for detecting and resolving Azure Firewall connection failures when using the Connection dialog   -->
      <add key="FirewallRuleDetectionEnabled" value="true"/>
      <!-- When DPI Awareness (configured in manifest file) and this setting are both enabled, .NET framework will handle the scaling of the built-in controls
             e.g. property grid's sort button, cursors, toolstrip button's images and treeview's state image
        -->
      <add key="EnableWindowsFormsHighDpiAutoResizing" value="true"/>
    </appSettings>
    <runtime>
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
        <probing privatePath="Extensions\Application;IDE\PublicAssemblies;IDE\PrivateAssemblies;IDE\ProjectComponents;IDE\Components;IDE\CommonExtensions\Microsoft\TemplateProviders;IDE\PrivateAssemblies\DataCollectors;IDE\PrivateAssemblies\DataCollectors\x86;IDE\StartPageAssemblies;IDE\CommonExtensions\Platform;IDE\CommonExtensions\Microsoft\Editor;IDE\CommonExtensions\Platform\Debugger;Mashup"/>
        <dependentAssembly>
          <assemblyIdentity name="Microsoft.SqlServer.XEvent.Linq" publicKeyToken="89845dcd8080cc91"/>
          <bindingRedirect oldVersion="14.0.0.0" newVersion="14.100.0.0"/>
        </dependentAssembly>
        <dependentAssembly>
          <assemblyIdentity name="Microsoft.SqlServer.XE.Core" publicKeyToken="89845dcd8080cc91"/>
          <bindingRedirect oldVersion="14.0.0.0" newVersion="14.100.0.0"/>
        </dependentAssembly>
      </assemblyBinding>
    </runtime>
    <!-- Necessary for loading up the new ico files -->
    <system.drawing bitmapSuffix=".VisualStudio.11.0" />
    <!-- Enhanced logging to help troubleshoot password loss issues -->
  </configuration>
```

```python
import clr
from System.Reflection import Assembly
import sys
sys.path.append(r"C:/Program Files (x86)/Microsoft SQL Server/140/Tools/Binn/ManagementStudio")
clr.AddReference(r"C:\\Program Files (x86)\\Microsoft SQL Server\\140\\Tools\\Binn\\ManagementStudio\\Microsoft.SqlServer.XEvent.Linq.dll")
from Microsoft.SqlServer.XEvent.Linq import QueryableXEventData
events = QueryableXEventData("C:\\Users\\Рома\\AppData\\Local\\Temp\\18_*.xel")
mm = {x.Name:{f.Name: f.Value for f in x.Fields} for x in events}
import pprint
pprint.pprint(mm)
```

```
{'audit_event': {'action_id': 1129534785,
                 'additional_information': '<action_info '
                                           'xmlns="http://schemas.microsoft.com/sqlserver/2008/sqlaudit_data"><session><![CDATA[SqlDbAuditing_ServerAudit$A_7A3CFF57-D915-48E8-9DAA-ACE6C581E0C4]]></session><action>event '
                                           'enabled</action><startup_type>automatic</startup_type><object><![CDATA[audit_event]]></object></action_info>',
                 'affected_rows': 0,
                 'application_name': '',
                 'audit_schema_version': 1,
                 'class_type': 8257,
                 'client_ip': 'Unknown',
                 'connection_id': <System.Guid object at 0x00D1C830>,
                 'database_name': '',
                 'database_principal_id': 0,
                 'database_principal_name': '',
                 'duration_milliseconds': 0,
                 'event_time': <System.DateTimeOffset object at 0x00D121D0>,
                 'is_column_permission': False,
                 'object_id': 0,
                 'object_name': '',
                 'permission_bitmask': <System.Byte[] object at 0x00D1C770>,
                 'response_rows': 0,
                 'schema_name': '',
                 'sequence_group_id': <System.Guid object at 0x00D1C790>,
                 'sequence_number': 1,
                 'server_instance_name': 'yasminserver',
                 'server_principal_id': 1,
                 'server_principal_name': 'sa',
                 'server_principal_sid': <System.Byte[] object at 0x00D1C7B0>,
                 'session_id': 99,
                 'session_server_principal_name': '',
                 'statement': '',
                 'succeeded': True,
                 'target_database_principal_id': 0,
                 'target_database_principal_name': '',
                 'target_server_principal_id': 0,
                 'target_server_principal_name': '',
                 'target_server_principal_sid': <System.Byte[] object at 0x00D1C7F0>,
                 'transaction_id': 0,
                 'user_defined_event_id': 0,
                 'user_defined_information': ''}}
```
