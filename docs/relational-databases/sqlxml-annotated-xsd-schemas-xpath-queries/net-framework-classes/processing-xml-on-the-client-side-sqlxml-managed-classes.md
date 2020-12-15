---
title: Elaborazione di XML sul lato client (SQLXML)
description: Informazioni su come elaborare il codice XML sul lato client usando la proprietà ClientSideXml dell'oggetto SqlXmlCommand nelle classi gestite SQLXML.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- processing XML on client side [SQLXML]
- client-side XML formatting
- Managed Classes [SQLXML], client-side XML formatting
- SQLXML Managed Classes, client-side XML formatting
- ClientSideXml property
ms.assetid: 5e7ecf18-66fc-49ff-bc50-83635cd7ac0b
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 42f55477c59b85945ccb1f0b776f9ab8ac2125b3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97430940"
---
# <a name="processing-xml-on-the-client-side-sqlxml-managed-classes"></a>Elaborazione di XML sul lato client (classi gestite SQLXML)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Questo esempio illustra l'uso della proprietà ClientSideXml. L'applicazione esegue una stored procedure nel server. Il risultato della stored procedure, ovvero un set di righe a due colonne, viene elaborato sul lato client per produrre un documento XML.  
  
 Il stored procedure GetContacts seguente restituisce **FirstName** e **LastName** dei dipendenti nella tabella Person. Contact del database AdventureWorks.  
  
```  
USE AdventureWorks  
CREATE PROCEDURE GetContacts @LastName varchar(20)  
AS  
SELECT FirstName, LastName  
FROM   Person.Contact  
WHERE LastName = @LastName  
Go  
```  
  
 Questa applicazione C# esegue il stored procedure e specifica l'opzione FOR XML AUTO in specificando il valore CommandText. Nell'applicazione, la proprietà ClientSideXml dell'oggetto SqlXmlCommand è impostata su true. In questo modo è possibile eseguire stored procedure preesistenti che restituiscono un set di righe e applicano a questo una trasformazione XML sul client.  
  
> [!NOTE]  
>  Nel codice è necessario specificare il nome dell'istanza di Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nella stringa di connessione.  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
    static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         //Stream strm;  
         SqlXmlParameter p;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.ClientSideXml = true;  
         cmd.CommandText = "EXEC GetContacts ? FOR XML NESTED";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         using (Stream strm = cmd.ExecuteStream())   
         {  
            using (StreamReader sr = new StreamReader(strm))  
                  {  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;  
      }  
  
public static int Main(String[] args)  
{  
    testParams();  
    return 0;  
}  
}  
```  
  
 Per testare questo esempio, è necessario che nel computer sia installato [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework.  
  
### <a name="to-test-the-application"></a>Per testare l'applicazione  
  
1.  Creare la stored procedure.  
  
2.  Salvare in una cartella il codice C# (DocSample.cs) fornito in questo esempio. Modificare il codice per specificare informazioni di accesso e sulla password appropriate.  
  
3.  Compilare il codice. Per compilare il codice al prompt dei comandi, utilizzare:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Viene creato un file eseguibile (DocSample.exe).  
  
4.  Al prompt dei comandi eseguire DocSample.exe.  

