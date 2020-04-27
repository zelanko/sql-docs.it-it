---
title: Avviso relativo all'utilizzo lato client di GEOMETRY, GEOGRAPHY e HIERARCHYID | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 500ee6b3-2154-45d2-a3cf-8760166d9413
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 524400e9c9420fb54447220215d4660874ec6d69
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091085"
---
# <a name="warning-about-client-side-usage-of-geometry-geography-and-hierarchyid"></a>Avviso relativo all'utilizzo sul lato client di GEOMETRY, GEOGRAPHY e HIERARCHYID
  L'assembly **Microsoft. SqlServer. Types. dll**, che contiene i tipi di dati spaziali, è stato aggiornato dalla versione 10,0 alla versione 11,0. È possibile che le applicazioni personalizzate che fanno riferimento a questo assembly abbiano esito negativo quando sussistono determinate condizioni.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 L'assembly **Microsoft. SqlServer. Types. dll**, che contiene i tipi di dati spaziali, è stato aggiornato dalla versione 10,0 alla versione 11,0. È possibile che le applicazioni personalizzate che fanno riferimento a questo assembly abbiano esito negativo quando sussistono le condizioni seguenti.  
  
-   Quando si sposta un'applicazione personalizzata da un computer in cui [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] è stato installato in un computer in cui [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è installato solo, l'applicazione avrà esito negativo perché la versione 10,0 dell'assembly **SqlTypes** a cui viene fatto riferimento non è presente. È possibile che venga visualizzato questo messaggio di errore: `"Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified."`  
  
-   Quando si fa riferimento all'assembly **SqlTypes** versione 11,0 e viene installata anche la versione 10,0, è possibile che venga visualizzato questo messaggio di errore:`"System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'."`  
  
-   Quando si fa riferimento all'assembly **SqlTypes** versione 11,0 da un'applicazione personalizzata destinata a .NET 3,5, 4 o 4,5, l'applicazione avrà esito negativo perché SqlClient per progettazione carica la versione 10,0 dell'assembly. Questo errore si verifica quando l'applicazione chiama uno dei metodi seguenti:  
  
    -   Metodo `GetValue` della classe `SqlDataReader`  
  
    -   Metodo `GetValues` della classe `SqlDataReader`  
  
    -   Operatore di indice parentesi quadre [] della classe `SqlDataReader`  
  
    -   Metodo `ExecuteScalar` della classe `SqlCommand`  
  
## <a name="corrective-action"></a>Azione correttiva  
 È possibile risolvere questo problema usando uno dei metodi seguenti:  
  
-   È possibile risolvere questo problema nel codice chiamando il metodo `GetSqlBytes`, anziché i metodi Get elencati in precedenza, per recuperare i tipi di sistema CLR di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], come illustrato nell'esempio seguente:  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   È possibile risolvere questo problema usando il reindirizzamento degli assembly nel file di configurazione dell'applicazione, come illustrato nell'esempio seguente:  
  
    ```xml  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    ```  
  
-   È possibile risolvere questo problema nella stringa di connessione specificando il valore "SQL Server 2012" per l'attributo "Type System Version" per forzare il caricamento della versione 11.0 dell'assembly da parte di SqlClient. Questo attributo della stringa di connessione è disponibile unicamente in .NET 4.5 e versioni successive.  
  
## <a name="see-also"></a>Vedi anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md
)  
  
  
