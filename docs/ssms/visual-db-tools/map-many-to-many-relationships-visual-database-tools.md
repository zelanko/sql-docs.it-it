---
title: Relazioni molti-a-molti
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], many-to-many
- junction tables [SQL Server]
- many-to-many relationships [SQL Server]
- mapping many-to-many relationships [SQL Server]
- database diagrams [SQL Server], relationships
ms.assetid: 2977cf92-98b5-48b2-b0fd-8fbc7040f2b4
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 63134fcbb7204bd701af073eee1bcaab22e68b05
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75224609"
---
# <a name="map-many-to-many-relationships-visual-database-tools"></a>Mapping di relazioni molti-a-molti (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Le relazioni molti-a-molti consentono di correlare ogni riga di una tabella con molte righe in un'altra tabella e viceversa. È possibile ad esempio creare una relazione molti-a-molti tra la tabella `authors` e la tabella `titles` per correlare ciascun autore con tutti i relativi libri e ciascun libro a tutti i relativi autori. Creando una relazione uno-a-molti da una delle tue tabelle, invece, si otterrebbe l'erronea indicazione che un libro può essere stato scritto da un solo autore o che ogni autore può scrivere un solo libro.  
  
Le relazioni molti-a-molti tra le tabelle vengono gestite nei database per mezzo delle tabelle di collegamento (junction table). Una tabella di collegamento contiene le colonne chiave primaria delle due tabelle da correlare. Successivamente si creerà una relazione dalle colonne chiave primaria di ognuna delle due tabelle alle corrispondenti colonne nella tabella di collegamento. Nel database pubs, la tabella `titleauthor` è una tabella di collegamento.  
  
### <a name="to-create-a-many-to-many-relationship-between-tables"></a>Per creare una relazione molti-a-molti tra tabelle  
  
1.  Nel diagramma del database aggiungere le tabelle tra cui si desidera creare una relazione molti-a-molti.  
  
2.  Fare clic con il pulsante destro del mouse sul diagramma e scegliere **Nuova tabella** dal menu di scelta rapida per creare una terza tabella, che diventerà la tabella di collegamento.  
  
3.  Nella finestra di dialogo **Scegli nome** modificare il nome di tabella assegnato automaticamente dal sistema. Ad esempio, la tabella di collegamento tra la tabella `titles` e la tabella `authors` ora si chiamerà `titleauthors`.  
  
4.  Copiare nella tabella di collegamento le colonne chiave primaria presenti nelle altre due tabelle. Così come per qualsiasi altra tabella, è possibile aggiungere delle colonne.  
  
5.  Nella tabella di collegamento impostare la chiave primaria in modo da includere tutte le colonne chiave primaria delle altre due tabelle. Per informazioni dettagliate, vedere [Procedura: Creare chiavi primarie (https://msdn.microsoft.com/85c623ca-4656-4d70-a9db-ee4d897cd214).  
  
6.  Definire una relazione uno-a-molti tra ciascuna delle due tabelle primarie e la tabella di collegamento. La tabella di collegamento dovrebbe essere sul lato "molti" di entrambe le relazioni create. Per informazioni dettagliate, vedere [Procedura: Creare relazioni tra tabelle (https://msdn.microsoft.com/867a54b8-5be4-46e6-9702-49ae6dabf67c).  
  
    > [!NOTE]  
    > La creazione di una tabella di collegamento in un diagramma di database non comporta l'inserimento dei dati dalle tabelle correlate nella tabella di collegamento. Per informazioni sull'inserimento di dati in una tabella, vedere [Creazione di query di accodamento &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-insert-results-queries-visual-database-tools.md).  
  
## <a name="see-also"></a>Vedere anche  
[Utilizzare diagrammi di database &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
