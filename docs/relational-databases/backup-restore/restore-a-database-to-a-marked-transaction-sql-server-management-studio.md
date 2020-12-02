---
title: Ripristinare il database fino a una transazione contrassegnata (SSMS)
description: Per il ripristino di un database di SQL Server usare la finestra di dialogo Ripristina log delle transazioni per ripristinare il database fino a una transazione contrassegnata nei backup del log disponibili.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoretlog.markedtransaction.f1
helpviewer_keywords:
- database restores [SQL Server], marked transactions
- restoring databases [SQL Server], marked transactions
- marked transactions [SQL Server], restoring
ms.assetid: 8f0ea144-1819-4832-905f-e5d0f49b066b
author: cawrites
ms.author: chadam
ms.openlocfilehash: d35f1478d3d9f290557a6eeebd6ce4365e461e21
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129127"
---
# <a name="restore-a-database-to-a-marked-transaction-sql-server-management-studio"></a>Ripristinare un database fino a una transazione contrassegnata (SQL Server Management Studio)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Quando un database è in stato di ripristino, è possibile usare la finestra di dialogo **Ripristina log delle transazioni** per ripristinare il database a una transazione contrassegnata nei backup del log disponibili.  
  
> [!NOTE]  
>  Per altre informazioni, vedere [Usare transazioni contrassegnate per recuperare coerentemente i database correlati &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) e [Recupero di database correlati che contengono transazioni contrassegnate](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md).  
  
### <a name="to-restore-a-marked-transaction"></a>Per ripristinare una transazione contrassegnata  
  
1.  Dopo aver stabilito la connessione all'istanza appropriata di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Esplora oggetti fare clic sul nome del server per espanderne l'albero.  
  
2.  Espandere **Database** e, a seconda del database, selezionare un database utente o espandere **Database di sistema** e selezionare un database di sistema.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività** e quindi fare clic su **Ripristina**.  
  
4.  Fare clic su **Log delle transazioni** per visualizzare la finestra di dialogo **Ripristina log delle transazioni** .  
  
5.  Nella sezione **Ripristina fino a** della pagina **Generale** fare clic su **Transazione contrassegnata** per visualizzare la finestra di dialogo **Seleziona transazione contrassegnata** . In tale finestra è visualizzata una griglia in cui sono elencate le transazioni contrassegnate disponibili nei backup dei log delle transazioni selezionati.  
  
     Per impostazione predefinita, il ripristino viene eseguito fino alla transazione contrassegnata esclusa. Per ripristinare anche la transazione contrassegnata, selezionare l'opzione **Includi transazione contrassegnata**.  
  
     Nella tabella seguente vengono elencate le intestazioni delle colonne della griglia con una descrizione dei rispettivi valori.  
  
    |Intestazione|valore|  
    |------------|-----------|  
    |\<blank>|Consente di visualizzare una casella di controllo per selezionare il contrassegno.|  
    |**Contrassegno transazione**|Nome della transazione contrassegnata specificato dall'utente durante l'esecuzione del commit della transazione.|  
    |**Data**|Data e ora assegnate alla transazione quando ne è stato eseguito il commit. Vengono visualizzate la data e l'ora della transazione registrate nella tabella **msdbgmarkhistory** , non nella data e ora del computer client.|  
    |**Descrizione**|Eventuale descrizione della transazione contrassegnata specificata dall'utente quando è stato eseguito il commit della transazione.|  
    |**LSN**|Numero di sequenza del file di log (LSN) della transazione contrassegnata.|  
    |**Database**|Nome del database in cui è stato eseguito il commit della transazione contrassegnata.|  
    |**Nome utente**|Nome dell'utente del database che ha eseguito il commit della transazione contrassegnata.|  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristinare un backup del database con SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
  
