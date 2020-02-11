---
title: Creazione di relazioni tra tabelle in un diagramma (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab36ebfefbfd3d8cee8e6da7caadf86eb4a10032
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63184274"
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>Creazione di relazioni tra tabelle in un diagramma (Visual Database Tools)
  È possibile creare relazioni tra le colonne in diverse tabelle in Progettazione diagrammi di database trascinando le colonne all'interno delle tabelle.  
  
### <a name="to-create-a-relationship-graphically"></a>Per creare una relazione graficamente  
  
1.  In Progettazione database fare clic sul selettore delle righe per una o più colonne di database che si desidera correlare a una colonna in un'altra tabella.  
  
2.  Trascinare la colonna o le colonne selezionate nella tabella correlata.  
  
3.  Verranno visualizzate due finestre di dialogo: **Relazione chiavi esterne** e **Tabelle e colonne**, quest'ultima visualizzata in primo piano.  
  
4.  Il nome della **relazione** ha un nome fornito dal sistema nel formato FK_*assegnato*_*foreignTable*. È possibile modificare questo valore.  
  
5.  Verificare che in **Tabella di chiave primaria** sia specificata la tabella corretta.  
  
6.  Nella griglia sono indicate le colonne locali e le colonne esterne corrispondenti. È possibile aggiungere o rimuovere le colonne di tabella o modificare i mapping.  
  
7.  Scegliere **OK**.  
  
     Verrà visualizzata la finestra di dialogo **Relazione chiavi esterne** . **Relazione selezionata** Mostra la relazione creata.  
  
8.  Modificare le proprietà della relazione nella griglia.  
  
9. Scegliere **OK** per creare la relazione.  
  
     Progettazione database mostra una relazione tra le colonne selezionate.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo tabelle e colonne &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Vincoli UNIQUE e check](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [Utilizzo di tabelle in diagrammi di database &#40;Visual Database Tools&#41;](work-with-tables-in-database-diagram-visual-database-tools.md)  
  
  
