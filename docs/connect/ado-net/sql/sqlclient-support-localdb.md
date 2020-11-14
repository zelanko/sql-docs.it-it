---
title: Supporto di SqlClient per Local DB
description: Descrive il supporto di SqlClient per i database Local DB.
ms.date: 08/15/2019
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 4760e4928421e0acdeca22f31a00cb148b82019c
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384370"
---
# <a name="sqlclient-support-for-localdb"></a>Supporto di SqlClient per Local DB

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

A partire da SQL Server con il nome in codice Denali, sarà disponibile una versione leggera di SQL Server denominata Local DB. Questo argomento illustra come connettersi a un database Local DB.  
  
## <a name="remarks"></a>Osservazioni  
Per altre informazioni su Local DB, inclusa la procedura per installare Local DB e configurare l'istanza di Local DB, vedere la documentazione online di SQL Server.  
  
Per riassumere le operazioni che è possibile eseguire con Local DB:  
  
- Creare e avviare istanze di Local DB con sqllocaldb.exe o il file app.config.  
  
- Usare sqlcmd.exe per aggiungere e modificare i database in un'istanza di Local DB. Ad esempio: `sqlcmd -S (localdb)\myinst`.  
  
- Usare la parola chiave della stringa di connessione `AttachDBFilename` per aggiungere un database all'istanza di Local DB. Quando si usa `AttachDBFilename`, se non viene specificato il nome del database con la parola chiave della stringa di connessione `Database`, il database sarà rimosso dall'istanza di Local DB alla chiusura dell'applicazione.  
  
- Specificare un'istanza di Local DB nella stringa di connessione. Ad esempio, se il nome dell'istanza è `myInstance`, la stringa di connessione includerà:  
  
```console
server=(localdb)\\myInstance  
```  
  
`User Instance=True` non è consentito quando ci si connette a un database Local DB.  
  
È possibile scaricare Local DB da [Microsoft SQL Server 2012 Feature Pack](https://www.microsoft.com/download/details.aspx?id=56041). Se si usa sqlcmd.exe per modificare i dati nell'istanza di Local DB, sarà necessario sqlcmd da SQL Server 2012, che è possibile ottenere anche da Microsoft SQL Server 2012 Feature Pack.  
  
## <a name="programmatically-create-a-named-instance"></a>Creare un'istanza denominata a livello di codice  
Un'applicazione può creare un'istanza denominata e specificare un database seguendo questa procedura:  
  
- Specificare le istanze di Local DB da creare nel file app.config come indicato di seguito.  Il numero di versione dell'istanza deve corrispondere al numero di versione dell'installazione di Local DB.  
  
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
  
- Specificare il nome dell'istanza usando la parola chiave della stringa di connessione `server`.  Il nome dell'istanza specificato nella parola chiave della stringa di connessione `server` deve corrispondere al nome specificato nel file app.config.  
  
- Usare la parola chiave della stringa di connessione `AttachDBFilename` per specificare il file con estensione mdf.  
  
## <a name="next-steps"></a>Passaggi successivi
- [Funzionalità di SQL Server e ADO.NET](sql-server-features-adonet.md)
