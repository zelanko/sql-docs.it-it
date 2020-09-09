---
title: 'Esempio: utilizzo del provider di eventi WMI in .NET'
description: Un'applicazione C# di esempio utilizza il provider di eventi WMI per restituire i dati degli eventi per tutti gli eventi di Data Definition Language che si verificano in un'istanza di SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Server Events, samples
- sample applications [WMI]
- managed code [WMI]
ms.assetid: 3d7aa7e9-0bb3-4a5b-9a3c-047f3240a6f8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ac51d05e79b11f35b264db4f23e5107f8de89b97
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539942"
---
# <a name="sample-using-the-wmi-event-provider-with-the-net-framework"></a>Esempio: Uso del provider di eventi WMI con .NET Framework
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Nell'esempio seguente viene creata un'applicazione in C# che utilizza il provider di eventi WMI per restituire dati degli eventi per tutti gli eventi DDL che si verificano in un'istanza dell'installazione predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Esempio  
 Per compilare l'esempio, utilizzare il file di comando seguente:  
  
```  
set compiler_path=C:\WINNT\Microsoft.NET\Framework\v2.0.50110  
  
%compiler_path%\csc %1  
```  
  
```  
using System;  
using System.Management;  
  
class SQLWEPExample   
{  
    public static void Main(string[] args)  
    {  
        string query =  @"SELECT * FROM DDL_EVENTS " ;  
        // Default namespace for default instance of SQL Server   
        string managementPath =  
            @"\\.\root\Microsoft\SqlServer\ServerEvents\MSSQLSERVER";  
        ManagementEventWatcher  watcher =   
            new ManagementEventWatcher(new WqlEventQuery (query));  
        ManagementScope scope = new ManagementScope (managementPath);  
        scope.Connect();  
        watcher.Scope = scope;  
        Console.WriteLine("Watching...");  
        while (true)  
        {  
            ManagementBaseObject obj = watcher.WaitForNextEvent();  
            Console.WriteLine("Event!");  
            foreach (PropertyData data in obj.Properties)  
            {  
                Console.Write("{0}:", data.Name);  
                if (data.Value == null)  
                {  
                    Console.WriteLine("<null>");  
                }  
                else  
                {  
                    Console.WriteLine(data.Value.ToString());  
                }  
            }  
            Console.WriteLine("-----");  
            Console.WriteLine();  
            Console.WriteLine();  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi al provider WMI per eventi del server](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
