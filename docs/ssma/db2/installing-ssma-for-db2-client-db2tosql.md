---
title: Installazione di SSMA per il client DB2 (DB2ToSQL) | Microsoft Docs
description: Informazioni sui prerequisiti di installazione per il client di SQL Server Migration Assistant (SSMA) per DB2 e su come installare.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4d069d7b34b590f8d2681a136f91ed327755d5a3
ms.sourcegitcommit: fd7b268a34562d70d46441f689543ecce7df2e4d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411619"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>Installazione di SSMA per il client DB2 (DB2ToSQL)

Il client SSMA è costituito dai file di programma che eseguono le attività seguenti:

- Connettersi a un database di DB2.
- Connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
- Convertire gli oggetti di database DB2 in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintassi.
- Caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
- Eseguire la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

In questo argomento vengono forniti i prerequisiti e le istruzioni per l'installazione di SSMA.

## <a name="prerequisites"></a>Prerequisiti

SSMA è progettato per funzionare con DB2 in z/OS versione 9,0 e 10,0, DB2 in LUW versione 9,8 e 10,1 o versioni successive, DB2 per i versione 7,1 o successiva e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 o versioni successive.

Prima di installare SSMA, verificare che il computer soddisfi i requisiti seguenti:

- Windows 7 o versioni successive o Windows Server 2008 o versioni successive.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o versioni successive.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] Versione 4.7.2 o successiva. È possibile ottenerlo dal [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882).
- Provider Microsoft OLE DB per DB2 versione 5 o successiva e connettività ai database DB2 di cui si vuole eseguire la migrazione.
- Accesso a e autorizzazioni sufficienti per il computer che ospita l'istanza di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure in cui si eseguirà la migrazione di dati e oggetti di database. Per ulteriori informazioni, vedere [connessione a SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).
- 4 GB di RAM consigliata.

## <a name="microsoft-ole-db-provider-for-db2"></a>Provider Microsoft OLE DB per DB2

Per scaricare la OLE DB provider per DB2 versione 6,0, passare a [Microsoft® SQL Server® 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992).

SSMA è un download Web. Per scaricare la versione più recente, vedere la [pagina di download SQL Server Migration Assistant](https://aka.ms/ssmafordb2).

Per installare il client di SSMA:

1. Fare doppio clic su **SSMAforDB2_*n*. msi**, dove *n* è il numero di Build.
2. Nella pagina di **benvenuto** selezionare **Avanti**.

   Se i prerequisiti non sono installati, verrà visualizzato un messaggio che indica che è necessario prima installare i componenti necessari. Assicurarsi di aver installato tutti i prerequisiti, quindi eseguire di nuovo il programma di installazione.

3. Leggere il contratto di licenza con l'utente finale. Se si accettano le condizioni, selezionare Accetto **il contratto**e quindi fare clic su **Avanti**.
4. Nella pagina Selezione **tipo di installazione** selezionare **tipico**.
5. Nella pagina **pronto per l'installazione** è possibile abilitare o disabilitare la telemetria e i controlli di aggiornamento automatici ogni volta che viene avviato lo strumento. Fare clic su **Installa** per avviare l'installazione.

> [!IMPORTANT]
> Disinstallare tutte le versioni precedenti di SSMA per DB2 prima di installare la nuova versione.

Il percorso di installazione predefinito è `C:\Program Files\Microsoft SQL Server Migration Assistant for DB2`.

## <a name="see-also"></a>Vedere anche

- [Installazione di componenti SSMA in SQL Server](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)
- [Migrazione di database DB2 a SQL Server](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)
