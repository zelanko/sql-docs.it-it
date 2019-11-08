---
title: Eseguire il backup e il ripristino di database con Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9176052b413293d25acd7696701e4f118adba03f
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595726"
---
# <a name="backup-and-restore-databases-using-always-encrypted"></a>Eseguire il backup e il ripristino di database con Always Encrypted 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Questo articolo descrive come eseguire il backup e il ripristino di un database contenente colonne protette con [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md).

Quando si esegue il backup di un database, il file di backup risultante contiene dati crittografati archiviati in colonne crittografate e tutti i metadati per le chiavi Always Encrypted.

Quando si ripristina un database, vengono ripristinati anche tutti i dati crittografati e tutti i metadati per le chiavi Always Encrypted. 

Se il database viene ripristinato in un altro server o con un nome diverso, non è necessario compiere alcuna operazione particolare per consentire all'applicazione di eseguire query sui dati crittografati nel database di destinazione, poiché le chiavi dei due database sono uguali.

Per informazioni dettagliate su come eseguire il backup e il ripristino di un database, vedere:
- [Panoramica del backup (SQL Server)](../../backup-restore/backup-overview-sql-server.md)
- [Ripristinare un database in un'istanza gestita](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started-restore)

## <a name="next-steps"></a>Next Steps
- [Eseguire query sulle colonne usando Always Encrypted con SQL Server Management Studio](always-encrypted-query-columns-ssms.md)
- [Sviluppare applicazioni usando Always Encrypted con enclave sicuri](always-encrypted-enclaves-client-development.md) 

## <a name="see-also"></a>Vedere anche
- [Crittografia sempre attiva](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Esportare e importare database usando Always Encrypted](always-encrypted-migrate-using-bacpac.md)
- [Eseguire la migrazione di dati da o verso colonne usando Always Encrypted con l'Importazione/Esportazione guidata SQL Server](always-encrypted-migrate-using-import-export-wizard.md)
- [Caricamento bulk di dati crittografati in colonne tramite Always Encrypted](migrate-sensitive-data-protected-by-always-encrypted.md)
