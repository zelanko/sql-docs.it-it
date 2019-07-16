---
title: Impostando le opzioni di migrazione (AccessToSQL) e conversione | Microsoft Docs
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3e89cfd6768aeedd970889cbaea46bb3e1ceae4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051503"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>Impostando le opzioni di migrazione (AccessToSQL) e conversione
Per ogni progetto SSMA, è possibile impostare le opzioni a livello di progetto. Queste opzioni specificano come gli oggetti vengono convertiti, migrazione dei dati e come eseguire il mapping tipi di dati di origine ai tipi di dati di destinazione. Prima di convertire gli oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure o eseguire la migrazione dei dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, verificare che le opzioni di configurazione siano appropriate per il progetto.  
  
## <a name="configuration-options-and-modes"></a>Le modalità e le opzioni di configurazione  
SSMA è quattro set di impostazioni di configurazione e quattro modalità per la configurazione di queste impostazioni: Per impostazione predefinita, ottimistica, backup completi e personalizzato. La modalità predefinita è consigliata per la maggior parte degli utenti. Utilizzare la modalità ottimistica per le conversioni semplici. Se si desidera vedere tutti i messaggi, usare la modalità completa. Nella modalità personalizzata, impostare le opzioni.  
  
Le impostazioni sono descritte nella sezione "Riferimenti dell'interfaccia utente" di questa documentazione. Per altre informazioni sulle impostazioni e come vengono applicate le impostazioni in ciascuna modalità, vedere gli argomenti seguenti:  
  
-   [Impostazioni progetto (conversione)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [Impostazioni progetto (migrazione)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [Impostazioni progetto (GUI)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Impostazioni progetto (mapping dei tipi)](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [Impostazioni progetto (SQL Azure)](https://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>Impostazione delle opzioni del progetto  
In SSMA, è possibile configurare le impostazioni predefinite per tutti i progetti. Queste impostazioni vengono salvate nel file di configurazione di SSMA e applicate a ogni nuovo progetto creato.  
  
**Per impostare le opzioni del progetto predefinito**  
  
1.  Nel **degli strumenti** dal menu **impostazioni di progetto predefinite**.  
  
2.  Nel **impostazioni di progetto predefinite** nella finestra di dialogo, effettuare una delle operazioni seguenti:  
  
    -   Seleziona tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati / modificato da **versione di destinazione della migrazione** elenco a discesa, fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi selezionare **Conversione o la migrazione o di SQL Azure**.  
  
        > [!NOTE]  
        > Opzione di SQL Azure è disponibile nel **generale** scheda solo se il tipo di progetto creato è SQL Azure.  
  
    -   Per selezionare una modalità predefinita, selezionare **predefinite**, **Optimistic**, o **completo** nel **modalità** casella di riepilogo a discesa.  
  
    -   Per specificare una modalità personalizzata, selezionare **personalizzati** nel **modalità** casella, selezionare un'opzione nel riquadro sinistro, fare clic sull'impostazione o un valore nel riquadro di destra e quindi selezionare o immettere il valore o la nuova impostazione.  
  
3.  Fare clic su **OK** per salvare le impostazioni.  
  
È anche possibile personalizzare le impostazioni per il progetto corrente. Queste impostazioni vengono salvate nel file di progetto corrente.  
  
**Per personalizzare le impostazioni per il progetto corrente**  
  
1.  Nel **degli strumenti** dal menu **le impostazioni del progetto**.  
  
2.  Nel **impostazioni del progetto** nella finestra di dialogo, effettuare una delle operazioni seguenti:  
  
    -   Per selezionare una modalità predefinita, selezionare **predefinite**, **Optimistic**, o **completo** nel **modalità** casella di riepilogo a discesa.  
  
    -   Per specificare una modalità personalizzata, selezionare **personalizzati** nel **modalità** casella, selezionare un'opzione nel riquadro sinistro, fare clic sull'impostazione o un valore nel riquadro di destra e quindi selezionare o immettere il valore o la nuova impostazione.  
  
3.  Fare clic su **OK** per salvare le impostazioni.  
  
## <a name="next-steps"></a>Passaggi successivi  
Il passaggio successivo nel processo di migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [Mapping tipi di origine e destinazione dati](mapping-source-and-target-data-types-accesstosql.md)  
  
-   Per personalizzare il mapping dei database di origine e destinazione, vedere [mapping dei database di origine e destinazione](mapping-source-and-target-databases-accesstosql.md)  
  
-   In caso contrario, è possibile convertire le definizioni degli oggetti di database di Access in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o le definizioni degli oggetti di SQL Azure. Per altre informazioni, vedere [la conversione di oggetti di Database di Access](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
