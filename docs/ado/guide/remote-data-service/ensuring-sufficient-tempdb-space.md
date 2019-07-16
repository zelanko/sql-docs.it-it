---
title: Garantire spazio sufficiente per TempDB | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe377cd15f2b95577a561e6784f78113b2843d07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922652"
---
# <a name="ensuring-sufficient-tempdb-space"></a>Garantire spazio sufficiente per TempDB
Se si verificano durante la gestione degli errori [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) gli oggetti che richiedono spazio su Microsoft SQL Server 6.5 di elaborazione, potrebbe essere necessario aumentare le dimensioni di TempDB. (Alcune query richiedono lo spazio di elaborazione temporaneo, ad esempio, una query con una clausola ORDER BY richiede una sorta del **Recordset**, che richiede spazio temporaneo.)  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!IMPORTANT]
>  Leggere questa procedura prima di eseguire le azioni poiché non è sufficiente compattare un dispositivo quando viene espanso.  
  
> [!NOTE]
>  Per inMicrosoft predefinita SQL Server 7.0 e versioni successive, database TempDB è impostato su aumenta automaticamente in base alle esigenze. Pertanto, questa procedura solo potrebbe essere necessaria nei server che eseguono versioni precedenti alla 7.0.  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>Per aumentare lo spazio di TempDB in SQL Server 6.5  
  
1.  Avviare Microsoft SQL Server Enterprise Manager, aprire l'albero per il Server e quindi aprire l'albero di dispositivi di Database.  
  
2.  Selezionare un dispositivo (fisico) per espandere, ad esempio Master e fare doppio clic sul dispositivo aprire il **modificare il dispositivo Database** nella finestra di dialogo.  
  
     Questa finestra di dialogo Mostra la quantità di spazio usano i database correnti.  
  
3.  Nel **dimensioni** casella, aumentare il dispositivo nella quantità desiderata (ad esempio, 50 megabyte (MB) di spazio su disco).  
  
4.  Fare clic su **Change Now** per aumentare la quantità di spazio in cui è possibile espandere il database temporaneo (logico).  
  
5.  Aprire la struttura di database nel server e quindi fare doppio clic su **TempDB** per aprire il **Modifica Database** nella finestra di dialogo. Il **Database** Elenca la quantità di spazio attualmente allocato in TempDB (**dimensione dati**). Per impostazione predefinita, questo è 2 MB.  
  
6.  Sotto il **dimensioni** gruppo, fare clic su **Espandi**. I grafici mostrano lo spazio disponibile e allocato in tutti i dispositivi fisici. Le barre di colore bordeaux rappresentano lo spazio disponibile.  
  
7.  Selezionare una **dispositivo Log**, ad esempio Master, per visualizzare le dimensioni disponibili nel **dimensioni (MB)** casella.  
  
8.  Fare clic su **espandere ora** per allocare lo spazio nel database TempDB.  
  
     Il **Modifica Database** nella finestra di dialogo consente di visualizzare la nuova dimensione allocata per il database TempDB.  
  
 Per altre informazioni su questo argomento, consultare il file della Guida di Microsoft SQL Server Enterprise Manager per la "Finestra di dialogo espandere Database".  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


