---
title: Impostazione delle opzioni di conversione e migrazione (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e074f603586afa0322d62872c49abb52fe47f047
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933962"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>Impostazione delle opzioni di conversione e migrazione (AccessToSQL)
Per ogni progetto SSMA, è possibile impostare le opzioni a livello di progetto. Queste opzioni specificano la modalità di conversione degli oggetti, la modalità di migrazione dei dati e la modalità di mapping dei tipi di dati di origine ai tipi di dati di destinazione. Prima di convertire o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure o migrare i dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, verificare che le opzioni di configurazione siano appropriate per il progetto.  
  
## <a name="configuration-options-and-modes"></a>Opzioni e modalità di configurazione  
SSMA prevede quattro set di impostazioni di configurazione e quattro modalità per la configurazione di queste impostazioni: predefinita, ottimistica, completa e personalizzata. La modalità predefinita è consigliata per la maggior parte degli utenti. Utilizzare la modalità ottimistica per le conversioni semplici. Utilizzare la modalità completa se si desidera visualizzare tutti i messaggi. In modalità personalizzata è possibile impostare le opzioni.  
  
Le impostazioni sono descritte nella sezione "Guida di riferimento all'interfaccia utente" della presente documentazione. Per ulteriori informazioni sulle impostazioni e sul modo in cui le impostazioni vengono applicate in ogni modalità, vedere gli argomenti seguenti:  
  
-   [Impostazioni progetto (conversione)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [Impostazioni progetto (migrazione)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [Impostazioni del progetto (interfaccia utente grafica)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Impostazioni progetto (mapping dei tipi)](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [Impostazioni progetto (SQL Azure)](https://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>Impostazione delle opzioni del progetto  
In SSMA è possibile configurare le impostazioni predefinite per tutti i progetti. Queste impostazioni vengono salvate nel file di configurazione SSMA e applicate a qualsiasi nuovo progetto creato.  
  
**Per impostare le opzioni predefinite del progetto**  
  
1.  Scegliere **Impostazioni progetto predefinite**dal menu **strumenti** .  
  
2.  Nella finestra di dialogo **Impostazioni progetto predefinite** eseguire una delle operazioni seguenti:  
  
    -   Selezionare il tipo di progetto di migrazione per il quale è necessario visualizzare/modificare le impostazioni dall'elenco a discesa della **versione di destinazione della migrazione** , fare clic su **generale** nella parte inferiore del riquadro sinistro, quindi selezionare **conversione o migrazione o SQL Azure**.  
  
        > [!NOTE]  
        > SQL Azure opzione è disponibile nella scheda **generale** solo se il tipo di progetto creato è SQL Azure.  
  
    -   Per selezionare una modalità predefinita, selezionare **predefinita**, **ottimistica**o **completa** nella casella di riepilogo a discesa **modalità** .  
  
    -   Per specificare una modalità personalizzata, selezionare **personalizzata** nella casella **modalità** , selezionare un'opzione nel riquadro a sinistra, fare clic sull'impostazione o sul valore nel riquadro destro, quindi selezionare o immettere il nuovo valore o impostazione.  
  
3.  Fare clic su **OK** per salvare le impostazioni.  
  
È inoltre possibile personalizzare le impostazioni per il progetto corrente. Queste impostazioni vengono salvate nel file di progetto corrente.  
  
**Per personalizzare le impostazioni per il progetto corrente**  
  
1.  Scegliere **Impostazioni progetto**dal menu **strumenti** .  
  
2.  Nella finestra di dialogo **Impostazioni progetto** eseguire una delle operazioni seguenti:  
  
    -   Per selezionare una modalità predefinita, selezionare **predefinita**, **ottimistica**o **completa** nella casella di riepilogo a discesa **modalità** .  
  
    -   Per specificare una modalità personalizzata, selezionare **personalizzata** nella casella **modalità** , selezionare un'opzione nel riquadro a sinistra, fare clic sull'impostazione o sul valore nel riquadro destro, quindi selezionare o immettere il nuovo valore o impostazione.  
  
3.  Fare clic su **OK** per salvare le impostazioni.  
  
## <a name="next-steps"></a>Passaggi successivi  
Il passaggio successivo della migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [mapping di tipi di dati di origine e di destinazione](mapping-source-and-target-data-types-accesstosql.md)  
  
-   Per personalizzare il mapping dei database di origine e di destinazione, vedere [mapping di database di origine e di destinazione](mapping-source-and-target-databases-accesstosql.md)  
  
-   In caso contrario, è possibile convertire le definizioni degli oggetti di database di Access in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure definizioni degli oggetti. Per ulteriori informazioni, vedere [conversione di oggetti di database di Access](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
