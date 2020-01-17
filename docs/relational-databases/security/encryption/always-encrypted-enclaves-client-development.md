---
title: Sviluppare applicazioni usando Always Encrypted con enclave sicuri | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7ec032a9a6bd6d02372d77d8844d5e4938fbe945
ms.sourcegitcommit: a26cb217adfbbfb3636dff43fb19a46462e2e994
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2019
ms.locfileid: "74492011"
---
# <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>Sviluppare applicazioni usando Always Encrypted con enclave sicuri
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[Always Encrypted con enclave sicuri](always-encrypted-enclaves.md) estende [Always Encrypted](always-encrypted-database-engine.md) per abilitare funzionalità più avanzate delle query dell'applicazione su colonne di database sensibili crittografate. Sfrutta le tecnologie basate sugli enclave sicuri per consentire all'executor della query in [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] di delegare i calcoli nelle colonne crittografate a un enclave sicuro all'interno del processo di [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

## <a name="client-driver-for-always-encrypted-with-secure-enclaves"></a>Driver client per Always Encrypted con enclave sicuri

Per sviluppare applicazioni usando Always Encrypted con enclave sicuri, è necessaria una versione del driver client di SQL che supporti enclave sicuri. Il driver client svolge il ruolo chiave seguente:
- Prima di inviare una query che usa un enclave sicuro a [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] per l'esecuzione, il driver avvia l'attestazione dell'enclave per verificare che l'enclave sicuro sia attendibile e possa essere usato senza problemi per elaborare i dati sensibili. Per altre informazioni sull'attestazione, vedere [Attestazione degli enclave sicuri](always-encrypted-enclaves.md#secure-enclave-attestation).
- Una volta completata l'attestazione, il driver client stabilisce una sessione sicura con l'enclave negoziando un segreto condiviso.
- Il driver usa il segreto condiviso per crittografare le chiavi di crittografia di colonna necessarie all'enclave per elaborare la query e invia le chiavi a [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], che le inoltra all'enclave sicuro che decrittografa le chiavi. 
- Il driver invia infine la query per l'esecuzione, che attiva i calcoli all'interno dell'enclave sicuro.

Per usare la funzionalità dell'enclave sicuro, è necessario configurare l'applicazione e il driver client per abilitare i calcoli dell'enclave durante la connessione al database e specificare un endpoint servizio di attestazione (un URL di attestazione dell'enclave) che punti a un servizio di attestazione per l'enclave. I dettagli dipendono dal driver e dal servizio/protocollo di attestazione in uso.

## <a name="next-steps"></a>Passaggi successivi

I driver client seguenti supportano Always Encrypted con enclave sicuri:
- Provider di dati .NET Framework per SQL Server in .NET Framework 4.7.2 o versione successiva. 
    - Per altre informazioni, vedere [Uso di Always Encrypted con il provider di dati .NET Framework per SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md).
    - Per un'esercitazione dettagliata, vedere [Esercitazione: Sviluppare un'applicazione .NET Framework usando Always Encrypted con enclave sicuri](../tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)
- Provider di dati Microsoft .NET per SQL Server in .NET Framework 4.6 o versione successiva e .NET Core 2.1 o versione successiva. 
    - Per altre informazioni, vedere [Uso di Always Encrypted con il provider di dati Microsoft .NET per SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md).
    - Per un'esercitazione dettagliata, vedere [Esercitazione: Sviluppare un'applicazione .NET usando Always Encrypted con enclave sicure](../../../connect/ado-net/sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)
- Microsoft ODBC Driver for SQL Server, versione 17.4 o successiva. 
    - Per altre informazioni, vedere [Using Always Encrypted with the Windows ODBC Driver](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) (Uso di Always Encrypted with the con il driver ODBC di Windows). 
    - Per informazioni su come abilitare i calcoli dell'enclave per una connessione di database usando ODBC, vedere la sezione [Abilitare Always Encrypted con enclave sicuri](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves).
