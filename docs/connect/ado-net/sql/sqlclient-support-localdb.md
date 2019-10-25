---
title: Supporto di SqlClient per Local DB
description: Viene descritto il supporto SqlClient per i database del database locale.
ms.date: 08/15/2019
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 14cbe4ccf227c9462d2a2dc19fb42d913ca7bc5a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451977"
---
# <a name="sqlclient-support-for-localdb"></a>Supporto di SqlClient per Local DB

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

A partire da SQL Server nome in codice Denali, sarà disponibile una versione semplificata di SQL Server, denominata local DB. In questo argomento viene illustrato come connettersi a un database del database locale.  
  
## <a name="remarks"></a>Remarks  
Per altre informazioni su Local DB, inclusa la procedura per installare Local DB e configurare l'istanza di Local DB, vedere la documentazione online di SQL Server.  
  
Per riepilogare le operazioni che è possibile eseguire con il database locale:  
  
- Creare e avviare le istanze del database locale con SqlLocalDB. exe o il file app. config.  
  
- Usare sqlcmd.exe per aggiungere e modificare i database in un'istanza di Local DB. Ad esempio, `sqlcmd -S (localdb)\myinst`.  
  
- Utilizzare la parola chiave della stringa di connessione `AttachDBFilename` per aggiungere un database all'istanza del database locale. Quando si usa `AttachDBFilename`, se non viene specificato il nome del database con la parola chiave della stringa di connessione `Database`, il database sarà rimosso dall'istanza di Local DB alla chiusura dell'applicazione.  
  
- Specificare un'istanza di Local DB nella stringa di connessione. Ad esempio, il nome dell'istanza è `myInstance`, la stringa di connessione includerà:  
  
```console
server=(localdb)\\myInstance  
```  
  
`User Instance=True` non è consentito quando ci si connette a un database del database locale.  
  
È possibile scaricare Local DB da [Microsoft SQL Server 2012 Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=29065). Se si usa sqlcmd.exe per modificare i dati nell'istanza di Local DB, sarà necessario sqlcmd da SQL Server 2012, che è possibile ottenere anche da Microsoft SQL Server 2012 Feature Pack.  
  
## <a name="programmatically-create-a-named-instance"></a>Creare un'istanza denominata a livello di codice  
Un'applicazione può creare un'istanza denominata e specificare un database come segue:  
  
- Specificare le istanze del database locale da creare nel file app. config, come indicato di seguito.  Il numero di versione dell'istanza deve essere uguale al numero di versione dell'installazione del database locale.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <configSections>  
        <section  
        name="system.data.localdb"  
        type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>  
      </configSections>  
      <system.data.localdb>  
        <localdbinstances>  
          <add name="myInstance" version="11.0" />  
        </localdbinstances>  
      </system.data.localdb>  
    </configuration>  
    ```  
  
- Specificare il nome dell'istanza utilizzando la parola chiave della stringa di connessione `server`.  Il nome dell'istanza specificato nella parola chiave della stringa di connessione `server` deve corrispondere al nome specificato nel file app.config.  
  
- Usare la parola chiave della stringa di connessione `AttachDBFilename` per specificare il. File MDF.  
  
## <a name="next-steps"></a>Passaggi successivi
- [Funzionalità di SQL Server e ADO.NET](sql-server-features-adonet.md)
